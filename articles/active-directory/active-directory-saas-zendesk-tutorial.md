---
title: "Didacticiel : Intégration d’Azure Active Directory à Zendesk | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Zendesk."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9d7c91e5-78f5-4016-862f-0f3242b00680
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: 46ccd57a4adeb810af459caaa1e592cf2b62cb8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zendesk"></a><span data-ttu-id="a0255-103">Didacticiel : Intégration d’Azure Active Directory à Zendesk</span><span class="sxs-lookup"><span data-stu-id="a0255-103">Tutorial: Azure Active Directory integration with Zendesk</span></span>

<span data-ttu-id="a0255-104">Dans ce didacticiel, vous apprendrez comment toointegrate Zendesk avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0255-104">In this tutorial, you learn how toointegrate Zendesk with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a0255-105">Intégration de Zendesk à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a0255-105">Integrating Zendesk with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a0255-106">Vous pouvez contrôler dans Azure AD qui a accès tooZendesk</span><span class="sxs-lookup"><span data-stu-id="a0255-106">You can control in Azure AD who has access tooZendesk</span></span>
- <span data-ttu-id="a0255-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooZendesk (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0255-107">You can enable your users tooautomatically get signed-on tooZendesk (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a0255-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a0255-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a0255-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a0255-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0255-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a0255-110">Prerequisites</span></span>

<span data-ttu-id="a0255-111">tooconfigure intégration d’Azure AD à Zendesk, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a0255-111">tooconfigure Azure AD integration with Zendesk, you need hello following items:</span></span>

- <span data-ttu-id="a0255-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0255-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a0255-113">Un abonnement pour lequel l’authentification unique à Zendesk est activée</span><span class="sxs-lookup"><span data-stu-id="a0255-113">A Zendesk single sign-on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="a0255-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a0255-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="a0255-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="a0255-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a0255-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a0255-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a0255-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a0255-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="a0255-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a0255-118">Scenario description</span></span>
<span data-ttu-id="a0255-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a0255-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a0255-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="a0255-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a0255-121">Ajout de Zendesk à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a0255-121">Adding Zendesk from hello gallery</span></span>
2. <span data-ttu-id="a0255-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0255-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zendesk-from-hello-gallery"></a><span data-ttu-id="a0255-123">Ajout de Zendesk à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a0255-123">Adding Zendesk from hello gallery</span></span>
<span data-ttu-id="a0255-124">tooconfigure hello intégration de Zendesk dans Azure AD, vous devez tooadd Zendesk à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a0255-124">tooconfigure hello integration of Zendesk into Azure AD, you need tooadd Zendesk from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a0255-125">**tooadd Zendesk à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a0255-125">**tooadd Zendesk from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0255-126">Bonjour  **[Azure Portal](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a0255-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a0255-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a0255-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a0255-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a0255-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a0255-131">Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="a0255-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a0255-133">Dans la zone de recherche de hello, tapez **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="a0255-133">In hello search box, type **Zendesk**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_search.png)

5. <span data-ttu-id="a0255-135">Dans le volet de résultats hello, sélectionnez **Zendesk**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a0255-135">In hello results panel, select **Zendesk**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a0255-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0255-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a0255-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zendesk, sur un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a0255-138">In this section, you configure and test Azure AD single sign-on with Zendesk based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="a0255-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Zendesk est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0255-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zendesk is tooa user in Azure AD.</span></span> <span data-ttu-id="a0255-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Zendesk doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="a0255-140">In other words, a link relationship between an Azure AD user and hello related user in Zendesk needs toobe established.</span></span>

<span data-ttu-id="a0255-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Zendesk.</span><span class="sxs-lookup"><span data-stu-id="a0255-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zendesk.</span></span>

<span data-ttu-id="a0255-142">tooconfigure et test Azure AD l’authentification unique à Zendesk, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="a0255-142">tooconfigure and test Azure AD single sign-on with Zendesk, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a0255-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a0255-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a0255-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a0255-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a0255-145">**[Création d’un utilisateur de test de Zendesk](#creating-a-zendesk-test-user)**  -toohave un équivalent de Britta Simon dans Zendesk est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a0255-145">**[Creating a Zendesk test user](#creating-a-zendesk-test-user)** - toohave a counterpart of Britta Simon in Zendesk that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a0255-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a0255-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a0255-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="a0255-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a0255-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0255-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a0255-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Zendesk.</span><span class="sxs-lookup"><span data-stu-id="a0255-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Zendesk application.</span></span>

<span data-ttu-id="a0255-150">**tooconfigure Azure AD single sign-on avec Zendesk, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a0255-150">**tooconfigure Azure AD single sign-on with Zendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0255-151">Bonjour portail Azure, sur hello **Zendesk** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a0255-151">In hello Azure portal, on hello **Zendesk** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a0255-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a0255-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_samlbase.png)

3. <span data-ttu-id="a0255-155">Sur hello **Zendesk domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a0255-155">On hello **Zendesk Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_url.png)

    <span data-ttu-id="a0255-157">a.</span><span class="sxs-lookup"><span data-stu-id="a0255-157">a.</span></span> <span data-ttu-id="a0255-158">Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="a0255-158">In hello **Sign-on URL** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    <span data-ttu-id="a0255-159">b.</span><span class="sxs-lookup"><span data-stu-id="a0255-159">b.</span></span> <span data-ttu-id="a0255-160">Bonjour **identificateur** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://<subdomain>.zendesk.com`</span><span class="sxs-lookup"><span data-stu-id="a0255-160">In hello **Identifier** textbox, type hello value using hello following pattern: `https://<subdomain>.zendesk.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a0255-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="a0255-161">These values are not real.</span></span> <span data-ttu-id="a0255-162">Mettre à jour ces valeurs avec l’URL de connexion réel hello et URL d’identificateur.</span><span class="sxs-lookup"><span data-stu-id="a0255-162">Update these values with hello actual Sign-on URL and Identifier URL.</span></span> <span data-ttu-id="a0255-163">Contact [équipe de support technique de Zendesk](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="a0255-163">Contact [Zendesk support team](https://support.zendesk.com/hc/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise) tooget these values.</span></span> 

4. <span data-ttu-id="a0255-164">Zendesk attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="a0255-164">Zendesk expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="a0255-165">Absence d’attribut SAML obligatoire, mais si vous le souhaitez, vous pouvez ajouter un attribut à partir de **attributs utilisateur** section par hello suivant étapes ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="a0255-165">There are no mandatory SAML attributes but optionally you can add an attribute from **User Attributes** section by following hello below steps:</span></span> 

     ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes1.png)

    <span data-ttu-id="a0255-167">a.</span><span class="sxs-lookup"><span data-stu-id="a0255-167">a.</span></span> <span data-ttu-id="a0255-168">Cliquez sur hello **afficher et modifier tous les hello autres attributs** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="a0255-168">Click hello **View and edit all hello other attributes** check box.</span></span>
     
    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_attributes2.png)
   
    <span data-ttu-id="a0255-170">b.</span><span class="sxs-lookup"><span data-stu-id="a0255-170">b.</span></span> <span data-ttu-id="a0255-171">Cliquez sur hello **ajouter un attribut** tooopen **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a0255-171">Click hello **Add Attribute** tooopen **Add attribute** dialog.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="a0255-173">c.</span><span class="sxs-lookup"><span data-stu-id="a0255-173">c.</span></span> <span data-ttu-id="a0255-174">Bonjour **nom** zone de texte, nom d’attribut de type hello (par exemple **emailaddress**).</span><span class="sxs-lookup"><span data-stu-id="a0255-174">In hello **Name** textbox, type hello attribute name (for example **emailaddress**).</span></span>
    
    <span data-ttu-id="a0255-175">d.</span><span class="sxs-lookup"><span data-stu-id="a0255-175">d.</span></span> <span data-ttu-id="a0255-176">À partir de hello **valeur** liste, la valeur de l’attribut select hello (en tant que **user.mail**).</span><span class="sxs-lookup"><span data-stu-id="a0255-176">From hello **Value** list, select hello attribute value (as **user.mail**).</span></span>
    
    <span data-ttu-id="a0255-177">e.</span><span class="sxs-lookup"><span data-stu-id="a0255-177">e.</span></span> <span data-ttu-id="a0255-178">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0255-178">Click **Ok**</span></span>
 
    > [!NOTE] 
    > <span data-ttu-id="a0255-179">Vous utilisez les attributs tooadd extension attributs qui ne sont pas dans Azure AD par défaut.</span><span class="sxs-lookup"><span data-stu-id="a0255-179">You use extension attributes tooadd attributes that are not in Azure AD by default.</span></span> <span data-ttu-id="a0255-180">Cliquez sur [les attributs d’utilisateur qui peuvent être définis dans SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello la liste complète des SAML attributs **Zendesk** accepte.</span><span class="sxs-lookup"><span data-stu-id="a0255-180">Click [User attributes that can be set in SAML](https://support.zendesk.com/hc/en-us/articles/203663676-Using-SAML-for-single-sign-on-Professional-and-Enterprise-) tooget hello complete list of SAML attributes that **Zendesk** accepts.</span></span> 

5. <span data-ttu-id="a0255-181">Sur hello **le certificat de signature SAML** section, hello de copie **l’empreinte numérique** valeur du certificat.</span><span class="sxs-lookup"><span data-stu-id="a0255-181">On hello **SAML Signing Certificate** section, copy hello **THUMBPRINT** value of certificate.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_certificate.png) 

6. <span data-ttu-id="a0255-183">Sur hello **Zendesk Configuration** , cliquez sur **configurer de Zendesk** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="a0255-183">On hello **Zendesk Configuration** section, click **Configure Zendesk** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a0255-184">Hello de copie **URL de déconnexion et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a0255-184">Copy hello **Sign-Out URL and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_configure.png) 

7. <span data-ttu-id="a0255-186">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Zendesk en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="a0255-186">In a different web browser window, log into your Zendesk company site as an administrator.</span></span>

8. <span data-ttu-id="a0255-187">Cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="a0255-187">Click **Admin**.</span></span>

9. <span data-ttu-id="a0255-188">Dans le volet de navigation gauche hello, cliquez sur **paramètres**, puis cliquez sur **sécurité**.</span><span class="sxs-lookup"><span data-stu-id="a0255-188">In hello left navigation pane, click **Settings**, and then click **Security**.</span></span>

10. <span data-ttu-id="a0255-189">Sur hello **sécurité** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a0255-189">On hello **Security** page, perform hello following steps:</span></span> 
   
     <span data-ttu-id="a0255-190">![Sécurité](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Sécurité")</span><span class="sxs-lookup"><span data-stu-id="a0255-190">![Security](./media/active-directory-saas-zendesk-tutorial/ic773089.png "Security")</span></span>

    <span data-ttu-id="a0255-191">![Authentification unique](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="a0255-191">![Single sign-on](./media/active-directory-saas-zendesk-tutorial/ic773090.png "Single sign-on")</span></span>

     <span data-ttu-id="a0255-192">a.</span><span class="sxs-lookup"><span data-stu-id="a0255-192">a.</span></span> <span data-ttu-id="a0255-193">Cliquez sur hello **administration et Agents** onglet.</span><span class="sxs-lookup"><span data-stu-id="a0255-193">Click hello **Admin & Agents** tab.</span></span>

     <span data-ttu-id="a0255-194">b.</span><span class="sxs-lookup"><span data-stu-id="a0255-194">b.</span></span> <span data-ttu-id="a0255-195">Sélectionnez **Single sign-on (SSO) and SAML**, puis **SAML**.</span><span class="sxs-lookup"><span data-stu-id="a0255-195">Select **Single sign-on (SSO) and SAML**, and then select **SAML**.</span></span>

     <span data-ttu-id="a0255-196">c.</span><span class="sxs-lookup"><span data-stu-id="a0255-196">c.</span></span> <span data-ttu-id="a0255-197">Dans **URL SSO SAML** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a0255-197">In **SAML SSO URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

     <span data-ttu-id="a0255-198">d.</span><span class="sxs-lookup"><span data-stu-id="a0255-198">d.</span></span> <span data-ttu-id="a0255-199">Dans **URL de déconnexion distante** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a0255-199">In **Remote Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
        
     <span data-ttu-id="a0255-200">e.</span><span class="sxs-lookup"><span data-stu-id="a0255-200">e.</span></span> <span data-ttu-id="a0255-201">Dans **empreinte numérique du certificat** zone de texte, collez hello **l’empreinte numérique** valeur de certificat que vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a0255-201">In **Certificate Fingerprint** textbox, paste hello **Thumbprint** value of certificate which you have copied from Azure portal.</span></span>
     
     <span data-ttu-id="a0255-202">f.</span><span class="sxs-lookup"><span data-stu-id="a0255-202">f.</span></span> <span data-ttu-id="a0255-203">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="a0255-203">Click **Save**.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a0255-204">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0255-204">Creating an Azure AD test user</span></span>
<span data-ttu-id="a0255-205">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="a0255-205">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a0255-207">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a0255-207">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0255-208">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a0255-208">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a0255-210">liste de hello toodisplay des utilisateurs Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a0255-210">toodisplay hello list of users go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a0255-212">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a0255-212">At hello top of hello dialog, click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a0255-214">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a0255-214">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zendesk-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a0255-216">a.</span><span class="sxs-lookup"><span data-stu-id="a0255-216">a.</span></span> <span data-ttu-id="a0255-217">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a0255-217">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a0255-218">b.</span><span class="sxs-lookup"><span data-stu-id="a0255-218">b.</span></span> <span data-ttu-id="a0255-219">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a0255-219">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a0255-220">c.</span><span class="sxs-lookup"><span data-stu-id="a0255-220">c.</span></span> <span data-ttu-id="a0255-221">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a0255-221">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a0255-222">d.</span><span class="sxs-lookup"><span data-stu-id="a0255-222">d.</span></span> <span data-ttu-id="a0255-223">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a0255-223">Click **Create**.</span></span> 

### <a name="creating-a-zendesk-test-user"></a><span data-ttu-id="a0255-224">Création d’un utilisateur de test Zendesk</span><span class="sxs-lookup"><span data-stu-id="a0255-224">Creating a Zendesk test user</span></span>

<span data-ttu-id="a0255-225">toolog d’utilisateurs tooenable Azure AD dans **Zendesk**, ils doivent être configurés dans **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="a0255-225">tooenable Azure AD users toolog into **Zendesk**, they must be provisioned into **Zendesk**.</span></span>  
<span data-ttu-id="a0255-226">En fonction du rôle hello affecté dans les applications hello, hello son comportement attendu :</span><span class="sxs-lookup"><span data-stu-id="a0255-226">Depending on hello role assigned in hello apps, it's hello expected behavior:</span></span>

 1. <span data-ttu-id="a0255-227">Les comptes de **l’utilisateur final** sont automatiquement approvisionnés lors de la connexion.</span><span class="sxs-lookup"><span data-stu-id="a0255-227">**End-user** accounts are automatically provisioned when signing in.</span></span>
 2. <span data-ttu-id="a0255-228">**Agent** et **Admin** comptes doivent toobe configuré manuellement dans **Zendesk** avant de vous connecter.</span><span class="sxs-lookup"><span data-stu-id="a0255-228">**Agent** and **Admin** accounts need toobe manually provisioned in **Zendesk** before signing in.</span></span>
 
<span data-ttu-id="a0255-229">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a0255-229">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0255-230">Connectez-vous à tooyour **Zendesk** client.</span><span class="sxs-lookup"><span data-stu-id="a0255-230">Log in tooyour **Zendesk** tenant.</span></span>

2. <span data-ttu-id="a0255-231">Sélectionnez hello **liste de clients** onglet.</span><span class="sxs-lookup"><span data-stu-id="a0255-231">Select hello **Customer List** tab.</span></span>

3. <span data-ttu-id="a0255-232">Sélectionnez hello **utilisateur** onglet, puis cliquez sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a0255-232">Select hello **User** tab, and click **Add**.</span></span>
   
    <span data-ttu-id="a0255-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span><span class="sxs-lookup"><span data-stu-id="a0255-233">![Add user](./media/active-directory-saas-zendesk-tutorial/ic773632.png "Add user")</span></span>
4. <span data-ttu-id="a0255-234">Tapez l’adresse de messagerie hello d’un compte Azure AD existant que vous souhaitez tooprovision, puis cliquez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a0255-234">Type hello email address of an existing Azure AD account you want tooprovision, and then click **Save**.</span></span>
   
    <span data-ttu-id="a0255-235">![Nouvel utilisateur](./media/active-directory-saas-zendesk-tutorial/ic773633.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="a0255-235">![New user](./media/active-directory-saas-zendesk-tutorial/ic773633.png "New user")</span></span>

> [!NOTE]
> <span data-ttu-id="a0255-236">Vous pouvez utiliser n’importe quel autre Zendesk utilisateur compte outil de création ou API fournie par Zendesk tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="a0255-236">You can use any other Zendesk user account creation tools or APIs provided by Zendesk tooprovision AAD user accounts.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a0255-237">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0255-237">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a0255-238">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooZendesk.</span><span class="sxs-lookup"><span data-stu-id="a0255-238">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooZendesk.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a0255-240">**tooassign Britta Simon tooZendesk, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a0255-240">**tooassign Britta Simon tooZendesk, perform hello following steps:**</span></span>

1. <span data-ttu-id="a0255-241">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a0255-241">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a0255-243">Dans la liste des applications hello, sélectionnez **Zendesk**.</span><span class="sxs-lookup"><span data-stu-id="a0255-243">In hello applications list, select **Zendesk**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zendesk-tutorial/tutorial_zendesk_app.png) 

3. <span data-ttu-id="a0255-245">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a0255-245">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a0255-247">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a0255-247">Click **Add** button.</span></span> <span data-ttu-id="a0255-248">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a0255-248">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a0255-250">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="a0255-250">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a0255-251">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a0255-251">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a0255-252">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a0255-252">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a0255-253">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a0255-253">Testing single sign-on</span></span>

<span data-ttu-id="a0255-254">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a0255-254">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a0255-255">Lorsque vous cliquez sur mosaïque Zendesk hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Zendesk application.</span><span class="sxs-lookup"><span data-stu-id="a0255-255">When you click hello Zendesk tile in hello Access Panel, you should get automatically signed-on tooyour Zendesk application.</span></span>
<span data-ttu-id="a0255-256">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a0255-256">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a0255-257">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a0255-257">Additional resources</span></span>

* [<span data-ttu-id="a0255-258">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0255-258">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a0255-259">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a0255-259">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zendesk-tutorial/tutorial_general_203.png
