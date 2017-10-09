---
title: "Didacticiel : Intégration d’Azure Active Directory avec Thirdlight | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et ThirdLight."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 168aae9a-54ee-4c2b-ab12-650a2c62b901
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: a510e514f6a8c4e89220b9a6f6db29668b451b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thirdlight"></a><span data-ttu-id="f12cf-103">Didacticiel : Intégration d’Azure Active Directory avec Thirdlight</span><span class="sxs-lookup"><span data-stu-id="f12cf-103">Tutorial: Azure Active Directory integration with ThirdLight</span></span>

<span data-ttu-id="f12cf-104">Dans ce didacticiel, vous apprendrez comment toointegrate ThirdLight avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f12cf-104">In this tutorial, you learn how toointegrate ThirdLight with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="f12cf-105">Intégration ThirdLight à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="f12cf-105">Integrating ThirdLight with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="f12cf-106">Vous pouvez contrôler dans Azure AD qui a accès tooThirdLight</span><span class="sxs-lookup"><span data-stu-id="f12cf-106">You can control in Azure AD who has access tooThirdLight</span></span>
- <span data-ttu-id="f12cf-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooThirdLight (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="f12cf-107">You can enable your users tooautomatically get signed-on tooThirdLight (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="f12cf-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="f12cf-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="f12cf-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="f12cf-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f12cf-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="f12cf-110">Prerequisites</span></span>

<span data-ttu-id="f12cf-111">tooconfigure intégration d’Azure AD avec ThirdLight, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="f12cf-111">tooconfigure Azure AD integration with ThirdLight, you need hello following items:</span></span>

- <span data-ttu-id="f12cf-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="f12cf-112">An Azure AD subscription</span></span>
- <span data-ttu-id="f12cf-113">Un abonnement Thirdlight pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="f12cf-113">A ThirdLight single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="f12cf-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="f12cf-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="f12cf-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="f12cf-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="f12cf-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f12cf-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="f12cf-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f12cf-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="f12cf-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="f12cf-118">Scenario description</span></span>
<span data-ttu-id="f12cf-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="f12cf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="f12cf-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="f12cf-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="f12cf-121">Ajout de ThirdLight à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f12cf-121">Adding ThirdLight from hello gallery</span></span>
2. <span data-ttu-id="f12cf-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f12cf-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thirdlight-from-hello-gallery"></a><span data-ttu-id="f12cf-123">Ajout de ThirdLight à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="f12cf-123">Adding ThirdLight from hello gallery</span></span>
<span data-ttu-id="f12cf-124">intégration de hello tooconfigure de ThirdLight dans Azure AD, vous devez tooadd ThirdLight à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="f12cf-124">tooconfigure hello integration of ThirdLight into Azure AD, you need tooadd ThirdLight from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="f12cf-125">**tooadd ThirdLight à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f12cf-125">**tooadd ThirdLight from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="f12cf-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f12cf-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="f12cf-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="f12cf-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="f12cf-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f12cf-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="f12cf-133">Dans la zone de recherche de hello, tapez **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-133">In hello search box, type **ThirdLight**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_search.png)

5. <span data-ttu-id="f12cf-135">Dans le volet de résultats hello, sélectionnez **ThirdLight**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="f12cf-135">In hello results panel, select **ThirdLight**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="f12cf-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f12cf-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="f12cf-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Thirdlight grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="f12cf-138">In this section, you configure and test Azure AD single sign-on with ThirdLight based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="f12cf-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans ThirdLight est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f12cf-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ThirdLight is tooa user in Azure AD.</span></span> <span data-ttu-id="f12cf-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ThirdLight doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="f12cf-140">In other words, a link relationship between an Azure AD user and hello related user in ThirdLight needs toobe established.</span></span>

<span data-ttu-id="f12cf-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="f12cf-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ThirdLight.</span></span>

<span data-ttu-id="f12cf-142">tooconfigure et test Azure AD l’authentification unique avec ThirdLight, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="f12cf-142">tooconfigure and test Azure AD single sign-on with ThirdLight, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="f12cf-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="f12cf-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="f12cf-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f12cf-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="f12cf-145">**[Création d’un utilisateur de test ThirdLight](#creating-a-thirdlight-test-user)**  -toohave un équivalent de Britta Simon dans ThirdLight est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f12cf-145">**[Creating a ThirdLight test user](#creating-a-thirdlight-test-user)** - toohave a counterpart of Britta Simon in ThirdLight that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="f12cf-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f12cf-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="f12cf-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="f12cf-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="f12cf-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="f12cf-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="f12cf-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="f12cf-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your ThirdLight application.</span></span>

<span data-ttu-id="f12cf-150">**tooconfigure Azure AD single sign-on avec ThirdLight, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f12cf-150">**tooconfigure Azure AD single sign-on with ThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f12cf-151">Bonjour portail Azure, sur hello **ThirdLight** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-151">In hello Azure portal, on hello **ThirdLight** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="f12cf-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="f12cf-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_samlbase.png)

3. <span data-ttu-id="f12cf-155">Sur hello **ThirdLight domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f12cf-155">On hello **ThirdLight Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_url.png)

    <span data-ttu-id="f12cf-157">a.</span><span class="sxs-lookup"><span data-stu-id="f12cf-157">a.</span></span> <span data-ttu-id="f12cf-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.thirdlight.com/`</span><span class="sxs-lookup"><span data-stu-id="f12cf-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/`</span></span>

    <span data-ttu-id="f12cf-159">b.</span><span class="sxs-lookup"><span data-stu-id="f12cf-159">b.</span></span> <span data-ttu-id="f12cf-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.thirdlight.com/saml/sp`</span><span class="sxs-lookup"><span data-stu-id="f12cf-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.thirdlight.com/saml/sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="f12cf-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="f12cf-161">These values are not real.</span></span> <span data-ttu-id="f12cf-162">Mettre à jour les valeurs de hello réel Identiifer et les URL de connexion.</span><span class="sxs-lookup"><span data-stu-id="f12cf-162">Update these values with hello actual Sign-On URL and Identiifer.</span></span> <span data-ttu-id="f12cf-163">Contact [équipe de support Client de ThirdLight](https://www.thirdlight.com/support) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="f12cf-163">Contact [ThirdLight Client support team](https://www.thirdlight.com/support) tooget these values.</span></span> 
 
4. <span data-ttu-id="f12cf-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="f12cf-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_certificate.png) 

5. <span data-ttu-id="f12cf-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="f12cf-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thirdlight-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="f12cf-168">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise tooyour ThirdLight en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f12cf-168">In a different web browser window, log in tooyour ThirdLight company site as an administrator.</span></span>

7. <span data-ttu-id="f12cf-169">Accédez trop**Configuration \> Administration système**, puis cliquez sur **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-169">Go too**Configuration \> System Administration**, and then click **SAML2**.</span></span>
   
    <span data-ttu-id="f12cf-170">![Administration système](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "Administration système")</span><span class="sxs-lookup"><span data-stu-id="f12cf-170">![System Administration](./media/active-directory-saas-thirdlight-tutorial/ic805843.png "System Administration")</span></span>

8. <span data-ttu-id="f12cf-171">Dans la section de configuration hello SAML2, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f12cf-171">In hello SAML2 configuration section, perform hello following steps:</span></span>
   
    <span data-ttu-id="f12cf-172">![Authentification unique SAML](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "Authentification unique SAML")</span><span class="sxs-lookup"><span data-stu-id="f12cf-172">![SAML Single Sign-On](./media/active-directory-saas-thirdlight-tutorial/ic805844.png "SAML Single Sign-On")</span></span>   

     <span data-ttu-id="f12cf-173">a.</span><span class="sxs-lookup"><span data-stu-id="f12cf-173">a.</span></span> <span data-ttu-id="f12cf-174">Sélectionnez **Enable SAML2 Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-174">Select **Enable SAML2 Single Sign-On**.</span></span>
 
     <span data-ttu-id="f12cf-175">b.</span><span class="sxs-lookup"><span data-stu-id="f12cf-175">b.</span></span> <span data-ttu-id="f12cf-176">Dans **Source for IdP Metadata**, sélectionnez **Load IdP Metadata from XML**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-176">As **Source for IdP Metadata**, select **Load IdP Metadata from XML**.</span></span>
 
     <span data-ttu-id="f12cf-177">c.</span><span class="sxs-lookup"><span data-stu-id="f12cf-177">c.</span></span> <span data-ttu-id="f12cf-178">Ouvrir le fichier de métadonnées téléchargé de hello, copier le contenu de hello, puis collez-le dans hello **XML des métadonnées IdP** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="f12cf-178">Open hello downloaded metadata file, copy hello content, and then paste it into hello **IdP Metadata XML** textbox.</span></span> 
     
     <span data-ttu-id="f12cf-179">d.</span><span class="sxs-lookup"><span data-stu-id="f12cf-179">d.</span></span> <span data-ttu-id="f12cf-180">Cliquez sur **Save SAML2 settings**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-180">Click **Save SAML2 settings**.</span></span>

> [!TIP]
> <span data-ttu-id="f12cf-181">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="f12cf-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="f12cf-182">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="f12cf-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="f12cf-183">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="f12cf-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="f12cf-184">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="f12cf-184">Creating an Azure AD test user</span></span>
<span data-ttu-id="f12cf-185">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="f12cf-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="f12cf-187">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f12cf-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="f12cf-188">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="f12cf-188">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="f12cf-190">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-190">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="f12cf-192">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="f12cf-192">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="f12cf-194">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f12cf-194">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-thirdlight-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="f12cf-196">a.</span><span class="sxs-lookup"><span data-stu-id="f12cf-196">a.</span></span> <span data-ttu-id="f12cf-197">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-197">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="f12cf-198">b.</span><span class="sxs-lookup"><span data-stu-id="f12cf-198">b.</span></span> <span data-ttu-id="f12cf-199">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="f12cf-199">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="f12cf-200">c.</span><span class="sxs-lookup"><span data-stu-id="f12cf-200">c.</span></span> <span data-ttu-id="f12cf-201">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-201">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="f12cf-202">d.</span><span class="sxs-lookup"><span data-stu-id="f12cf-202">d.</span></span> <span data-ttu-id="f12cf-203">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-203">Click **Create**.</span></span>
 
### <a name="creating-a-thirdlight-test-user"></a><span data-ttu-id="f12cf-204">Création d’un utilisateur de test Thirdlight</span><span class="sxs-lookup"><span data-stu-id="f12cf-204">Creating a ThirdLight test user</span></span>

<span data-ttu-id="f12cf-205">tooenable Azure AD les utilisateurs toolog dans tooThirdLight, vous devez les configurer dans ThirdLight.</span><span class="sxs-lookup"><span data-stu-id="f12cf-205">tooenable Azure AD users toolog in tooThirdLight, they must be provisioned into ThirdLight.</span></span>  
<span data-ttu-id="f12cf-206">Dans les cas de hello de ThirdLight, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="f12cf-206">In hello case of ThirdLight, provisioning is a manual task.</span></span>

<span data-ttu-id="f12cf-207">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f12cf-207">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="f12cf-208">Connectez-vous à tooyour **ThirdLight** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="f12cf-208">Log in tooyour **ThirdLight** company site as an administrator.</span></span>

2. <span data-ttu-id="f12cf-209">Accédez trop**utilisateurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="f12cf-209">Go too**Users** tab.</span></span>

3. <span data-ttu-id="f12cf-210">Sélectionnez **Users and Groups**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-210">Select **Users and Groups**.</span></span>

4. <span data-ttu-id="f12cf-211">Cliquez sur le bouton **Add new User** .</span><span class="sxs-lookup"><span data-stu-id="f12cf-211">Click **Add new User** button.</span></span>

5. <span data-ttu-id="f12cf-212">Entrez **hello nom d’utilisateur, nom ou Description, courrier électronique, choisissez une présélection ou nouveaux membres du groupe** d’un compte AAD valide que vous souhaitez tooprovision.</span><span class="sxs-lookup"><span data-stu-id="f12cf-212">Enter **hello Username, Name or Description, Email, Choose a Preset or Group of New Members** of a valid AAD account you want tooprovision.</span></span>

6. <span data-ttu-id="f12cf-213">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-213">Click **Create**.</span></span>

>[!NOTE]
><span data-ttu-id="f12cf-214">Vous pouvez utiliser n’importe quel autre Thirdlight utilisateur compte outil de création ou API fournie par Thirdlight tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="f12cf-214">You can use any other Thirdlight user account creation tools or APIs provided by Thirdlight tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="f12cf-215">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="f12cf-215">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="f12cf-216">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooThirdLight.</span><span class="sxs-lookup"><span data-stu-id="f12cf-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThirdLight.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="f12cf-218">**tooassign Britta Simon tooThirdLight, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="f12cf-218">**tooassign Britta Simon tooThirdLight, perform hello following steps:**</span></span>

1. <span data-ttu-id="f12cf-219">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="f12cf-221">Dans la liste des applications hello, sélectionnez **ThirdLight**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-221">In hello applications list, select **ThirdLight**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-thirdlight-tutorial/tutorial_thirdlight_app.png) 

3. <span data-ttu-id="f12cf-223">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="f12cf-225">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-225">Click **Add** button.</span></span> <span data-ttu-id="f12cf-226">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="f12cf-228">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="f12cf-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="f12cf-229">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="f12cf-230">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="f12cf-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="f12cf-231">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="f12cf-231">Testing single sign-on</span></span>

<span data-ttu-id="f12cf-232">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="f12cf-232">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="f12cf-233">Lorsque vous cliquez sur mosaïque ThirdLight hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour ThirdLight application.</span><span class="sxs-lookup"><span data-stu-id="f12cf-233">When you click hello ThirdLight tile in hello Access Panel, you should get automatically signed-on tooyour ThirdLight application.</span></span>
<span data-ttu-id="f12cf-234">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="f12cf-234">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="f12cf-235">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f12cf-235">Additional resources</span></span>

* [<span data-ttu-id="f12cf-236">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f12cf-236">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="f12cf-237">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="f12cf-237">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thirdlight-tutorial/tutorial_general_203.png

