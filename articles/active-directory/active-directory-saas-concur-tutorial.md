---
title: "Didacticiel : Intégration d’Azure Active Directory à Concur | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Concur."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1eee0a5d-24fa-4986-9aef-3c543cfe3296
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 1012bf8c6f036306d0ca90689415d5e22e449989
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-concur"></a><span data-ttu-id="17a1b-103">Didacticiel : Intégration d’Azure Active Directory à Concur</span><span class="sxs-lookup"><span data-stu-id="17a1b-103">Tutorial: Azure Active Directory integration with Concur</span></span>

<span data-ttu-id="17a1b-104">Dans ce didacticiel, vous apprendrez comment toointegrate Concur avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="17a1b-104">In this tutorial, you learn how toointegrate Concur with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="17a1b-105">Intégration de Concur à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="17a1b-105">Integrating Concur with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="17a1b-106">Vous pouvez contrôler dans Azure AD qui a accès tooConcur</span><span class="sxs-lookup"><span data-stu-id="17a1b-106">You can control in Azure AD who has access tooConcur</span></span>
- <span data-ttu-id="17a1b-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooConcur (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="17a1b-107">You can enable your users tooautomatically get signed-on tooConcur (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="17a1b-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="17a1b-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="17a1b-109">Si vous souhaitez tooknow plus d’informations sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="17a1b-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="17a1b-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="17a1b-110">Prerequisites</span></span>

<span data-ttu-id="17a1b-111">tooconfigure intégration d’Azure AD à Concur, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="17a1b-111">tooconfigure Azure AD integration with Concur, you need hello following items:</span></span>

- <span data-ttu-id="17a1b-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="17a1b-112">An Azure AD subscription</span></span>
- <span data-ttu-id="17a1b-113">Un abonnement Concur pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="17a1b-113">A Concur single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="17a1b-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="17a1b-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="17a1b-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="17a1b-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="17a1b-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="17a1b-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="17a1b-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="17a1b-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="17a1b-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="17a1b-118">Scenario description</span></span>
<span data-ttu-id="17a1b-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="17a1b-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="17a1b-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="17a1b-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="17a1b-121">Ajout de Concur à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="17a1b-121">Adding Concur from hello gallery</span></span>
2. <span data-ttu-id="17a1b-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="17a1b-122">Configuring and testing Azure AD single sign-on</span></span>

>[!NOTE]
><span data-ttu-id="17a1b-123">configuration de Hello de votre abonnement Concur pour l’authentification unique fédérée via SAML est une tâche distincte, ce qui vous devez contacter [équipe de support Client de Concur](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="17a1b-123">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 

## <a name="adding-concur-from-hello-gallery"></a><span data-ttu-id="17a1b-124">Ajout de Concur à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="17a1b-124">Adding Concur from hello gallery</span></span>
<span data-ttu-id="17a1b-125">intégration de hello tooconfigure de Concur dans Azure AD, vous devez tooadd Concur à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="17a1b-125">tooconfigure hello integration of Concur into Azure AD, you need tooadd Concur from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="17a1b-126">**tooadd Concur à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="17a1b-126">**tooadd Concur from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="17a1b-127">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="17a1b-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="17a1b-129">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="17a1b-130">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-130">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="17a1b-132">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="17a1b-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="17a1b-134">Dans la zone de recherche de hello, tapez **Concur**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-134">In hello search box, type **Concur**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_search.png)

5. <span data-ttu-id="17a1b-136">Dans le volet de résultats hello, sélectionnez **Concur**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="17a1b-136">In hello results panel, select **Concur**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-concur-tutorial/tutorial_concur_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="17a1b-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="17a1b-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="17a1b-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Concur avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="17a1b-139">In this section, you configure and test Azure AD single sign-on with Concur based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="17a1b-140">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Concur est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="17a1b-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Concur is tooa user in Azure AD.</span></span> <span data-ttu-id="17a1b-141">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Concur doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="17a1b-141">In other words, a link relationship between an Azure AD user and hello related user in Concur needs toobe established.</span></span>

<span data-ttu-id="17a1b-142">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Concur.</span><span class="sxs-lookup"><span data-stu-id="17a1b-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Concur.</span></span>

<span data-ttu-id="17a1b-143">tooconfigure et test Azure AD l’authentification unique avec Concur, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="17a1b-143">tooconfigure and test Azure AD single sign-on with Concur, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="17a1b-144">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="17a1b-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="17a1b-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="17a1b-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="17a1b-146">**[Création d’un utilisateur de test de Concur](#creating-a-concur-test-user)**  -toohave un équivalent de Britta Simon dans Concur est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="17a1b-146">**[Creating a Concur test user](#creating-a-concur-test-user)** - toohave a counterpart of Britta Simon in Concur that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="17a1b-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="17a1b-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="17a1b-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="17a1b-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="17a1b-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="17a1b-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="17a1b-150">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Concur.</span><span class="sxs-lookup"><span data-stu-id="17a1b-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Concur application.</span></span>

<span data-ttu-id="17a1b-151">**tooconfigure Azure AD single sign-on avec Concur, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="17a1b-151">**tooconfigure Azure AD single sign-on with Concur, perform hello following steps:**</span></span>

1. <span data-ttu-id="17a1b-152">Bonjour portail Azure, sur hello **Concur** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-152">In hello Azure portal, on hello **Concur** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="17a1b-154">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="17a1b-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-concur-tutorial/tutorial_concur_samlbase.png)

3. <span data-ttu-id="17a1b-156">Sur hello **approuvent le domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="17a1b-156">On hello **Concur Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-concur-tutorial/tutorial_concur_url.png)

    <span data-ttu-id="17a1b-158">a.</span><span class="sxs-lookup"><span data-stu-id="17a1b-158">a.</span></span> <span data-ttu-id="17a1b-159">Bonjour **URL de connexion** zone de texte, valeur hello de type hello suivant le modèle à l’aide de :`https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span><span class="sxs-lookup"><span data-stu-id="17a1b-159">In hello **Sign on URL** textbox, type hello value using hello following pattern: `https://www.concursolutions.com/UI/SSO/<OrganizationId>`</span></span>

    <span data-ttu-id="17a1b-160">b.</span><span class="sxs-lookup"><span data-stu-id="17a1b-160">b.</span></span> <span data-ttu-id="17a1b-161">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<customer-domain>.concursolutions.com`</span><span class="sxs-lookup"><span data-stu-id="17a1b-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<customer-domain>.concursolutions.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="17a1b-162">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="17a1b-162">These values are not hello real.</span></span> <span data-ttu-id="17a1b-163">Mise à jour ces valeurs avec hello réel connectent URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="17a1b-163">Update these values with hello actual Sign on URL and Identifier.</span></span> <span data-ttu-id="17a1b-164">Contact [équipe de support Client de Concur](https://www.concur.co.in/contact) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="17a1b-164">Contact [Concur Client support team](https://www.concur.co.in/contact) tooget these values.</span></span> 

4. <span data-ttu-id="17a1b-165">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="17a1b-165">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-concur-tutorial/tutorial_concur_certificate.png) 

5. <span data-ttu-id="17a1b-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="17a1b-167">Click **Save** button.</span></span>

    <span data-ttu-id="17a1b-168">![Configurer l’authentification unique](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span><span class="sxs-lookup"><span data-stu-id="17a1b-168">![Configure Single Sign-On](./media/active-directory-saas-concur-tutorial/tutorial_general_400.png)
<CS></span></span>

6. <span data-ttu-id="17a1b-169">tooconfigure l’authentification unique sur **Concur** côté, vous devez hello toosend téléchargé **Metadata XML** prise en charge tooConcur.</span><span class="sxs-lookup"><span data-stu-id="17a1b-169">tooconfigure single sign-on on **Concur** side, you need toosend hello downloaded **Metadata XML** tooConcur support.</span></span> <span data-ttu-id="17a1b-170">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="17a1b-170">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

  >[!NOTE]
  ><span data-ttu-id="17a1b-171">configuration de Hello de votre abonnement Concur pour l’authentification unique fédérée via SAML est une tâche distincte, ce qui vous devez contacter [équipe de support Client de Concur](https://www.concur.co.in/contact) tooperform.</span><span class="sxs-lookup"><span data-stu-id="17a1b-171">hello configuration of your Concur subscription for federated SSO via SAML is a separate task, which you must contact [Concur Client support team](https://www.concur.co.in/contact) tooperform.</span></span> 
  
<CE>

> [!TIP]
> <span data-ttu-id="17a1b-172">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="17a1b-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="17a1b-173">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="17a1b-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="17a1b-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="17a1b-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="17a1b-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="17a1b-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="17a1b-176">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="17a1b-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="17a1b-178">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="17a1b-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="17a1b-179">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="17a1b-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="17a1b-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="17a1b-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="17a1b-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="17a1b-185">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="17a1b-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-concur-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="17a1b-187">a.</span><span class="sxs-lookup"><span data-stu-id="17a1b-187">a.</span></span> <span data-ttu-id="17a1b-188">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="17a1b-189">b.</span><span class="sxs-lookup"><span data-stu-id="17a1b-189">b.</span></span> <span data-ttu-id="17a1b-190">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="17a1b-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="17a1b-191">c.</span><span class="sxs-lookup"><span data-stu-id="17a1b-191">c.</span></span> <span data-ttu-id="17a1b-192">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="17a1b-193">d.</span><span class="sxs-lookup"><span data-stu-id="17a1b-193">d.</span></span> <span data-ttu-id="17a1b-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-194">Click **Create**.</span></span>
 
### <a name="creating-a-concur-test-user"></a><span data-ttu-id="17a1b-195">Création d’un utilisateur de test Concur</span><span class="sxs-lookup"><span data-stu-id="17a1b-195">Creating a Concur test user</span></span>

<span data-ttu-id="17a1b-196">Application prend en charge hello juste configuration en temps utilisateur et une fois que les utilisateurs de l’authentification sont créés automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="17a1b-196">Application supports hello Just in time user provisioning and after authentication users are created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="17a1b-197">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="17a1b-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="17a1b-198">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooConcur.</span><span class="sxs-lookup"><span data-stu-id="17a1b-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooConcur.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="17a1b-200">**tooassign Britta Simon tooConcur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="17a1b-200">**tooassign Britta Simon tooConcur, perform hello following steps:**</span></span>

1. <span data-ttu-id="17a1b-201">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="17a1b-203">Dans la liste des applications hello, sélectionnez **Concur**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-203">In hello applications list, select **Concur**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-concur-tutorial/tutorial_concur_app.png) 

3. <span data-ttu-id="17a1b-205">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="17a1b-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-207">Click **Add** button.</span></span> <span data-ttu-id="17a1b-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="17a1b-210">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="17a1b-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="17a1b-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="17a1b-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="17a1b-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="17a1b-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="17a1b-213">Testing single sign-on</span></span>

<span data-ttu-id="17a1b-214">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="17a1b-214">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="17a1b-215">Lorsque vous cliquez sur mosaïque Concur hello hello volet d’accès, vous devez obtenir la page de connexion de l’application de Concur.</span><span class="sxs-lookup"><span data-stu-id="17a1b-215">When you click hello Concur tile in hello Access Panel, you should get login page of Concur application.</span></span>
<span data-ttu-id="17a1b-216">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="17a1b-216">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="17a1b-217">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="17a1b-217">Additional resources</span></span>

* [<span data-ttu-id="17a1b-218">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="17a1b-218">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="17a1b-219">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="17a1b-219">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="17a1b-220">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="17a1b-220">Configure User Provisioning</span></span>](active-directory-saas-concur-provisioning-tutorial.md)



<!--Image references-->

[1]: ./media/active-directory-saas-concur-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-concur-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-concur-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-concur-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-concur-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-concur-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-concur-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-concur-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-concur-tutorial/tutorial_general_203.png

