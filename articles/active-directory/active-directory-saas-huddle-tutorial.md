---
title: "Didacticiel : Intégration d’Azure Active Directory avec Huddle | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Huddle."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8389ba4c-f5f8-4ede-b2f4-32eae844ceb0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 0b2f6c4d839943cdd07699a1ff95dc8f90505699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-huddle"></a><span data-ttu-id="073c4-103">Didacticiel : Intégration d’Azure Active Directory avec Huddle</span><span class="sxs-lookup"><span data-stu-id="073c4-103">Tutorial: Azure Active Directory integration with Huddle</span></span>

<span data-ttu-id="073c4-104">Dans ce didacticiel, vous apprendrez comment toointegrate Huddle avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="073c4-104">In this tutorial, you learn how toointegrate Huddle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="073c4-105">Intégration de Huddle à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="073c4-105">Integrating Huddle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="073c4-106">Vous pouvez contrôler dans Azure AD qui a accès tooHuddle</span><span class="sxs-lookup"><span data-stu-id="073c4-106">You can control in Azure AD who has access tooHuddle</span></span>
- <span data-ttu-id="073c4-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHuddle (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="073c4-107">You can enable your users tooautomatically get signed-on tooHuddle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="073c4-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="073c4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="073c4-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="073c4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="073c4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="073c4-110">Prerequisites</span></span>

<span data-ttu-id="073c4-111">intégration de tooconfigure Azure AD à Huddle, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="073c4-111">tooconfigure Azure AD integration with Huddle, you need hello following items:</span></span>

- <span data-ttu-id="073c4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="073c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="073c4-113">Un abonnement Huddle pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="073c4-113">A Huddle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="073c4-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="073c4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="073c4-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="073c4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="073c4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="073c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="073c4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="073c4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="073c4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="073c4-118">Scenario description</span></span>

<span data-ttu-id="073c4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="073c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="073c4-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="073c4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="073c4-121">Ajout de Huddle à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="073c4-121">Adding Huddle from hello gallery</span></span>
2. <span data-ttu-id="073c4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="073c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-huddle-from-hello-gallery"></a><span data-ttu-id="073c4-123">Ajout de Huddle à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="073c4-123">Adding Huddle from hello gallery</span></span>
<span data-ttu-id="073c4-124">intégration de hello tooconfigure de Huddle dans Azure AD, vous devez tooadd Huddle à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="073c4-124">tooconfigure hello integration of Huddle into Azure AD, you need tooadd Huddle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="073c4-125">**tooadd Huddle à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="073c4-125">**tooadd Huddle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="073c4-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="073c4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="073c4-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="073c4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="073c4-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="073c4-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="073c4-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="073c4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="073c4-133">Dans la zone de recherche de hello, tapez **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="073c4-133">In hello search box, type **Huddle**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_search.png)

5. <span data-ttu-id="073c4-135">Dans le volet de résultats hello, sélectionnez **Huddle**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="073c4-135">In hello results panel, select **Huddle**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="073c4-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="073c4-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="073c4-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Huddle avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="073c4-138">In this section, you configure and test Azure AD single sign-on with Huddle based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="073c4-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Huddle est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="073c4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Huddle is tooa user in Azure AD.</span></span> <span data-ttu-id="073c4-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Huddle besoins toobe est établie.</span><span class="sxs-lookup"><span data-stu-id="073c4-140">In other words, a link relationship between an Azure AD user and hello related user in Huddle needs toobe established.</span></span>

<span data-ttu-id="073c4-141">Dans Huddle, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="073c4-141">In Huddle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="073c4-142">tooconfigure et test Azure AD l’authentification unique avec Huddle, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="073c4-142">tooconfigure and test Azure AD single sign-on with Huddle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="073c4-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="073c4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>

2. <span data-ttu-id="073c4-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="073c4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>

3. <span data-ttu-id="073c4-145">**[Création d’un utilisateur de test de Huddle](#creating-a-huddle-test-user)**  -toohave un équivalent de Britta Simon dans Huddle est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="073c4-145">**[Creating a Huddle test user](#creating-a-huddle-test-user)** - toohave a counterpart of Britta Simon in Huddle that is linked toohello Azure AD representation of user.</span></span>

4. <span data-ttu-id="073c4-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="073c4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>

5. <span data-ttu-id="073c4-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="073c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="073c4-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="073c4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="073c4-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de Huddle.</span><span class="sxs-lookup"><span data-stu-id="073c4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Huddle application.</span></span>

<span data-ttu-id="073c4-150">**tooconfigure Azure AD l’authentification unique avec Huddle, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="073c4-150">**tooconfigure Azure AD single sign-on with Huddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="073c4-151">Bonjour portail Azure, sur hello **Huddle** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="073c4-151">In hello Azure portal, on hello **Huddle** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="073c4-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="073c4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_samlbase.png)

3. <span data-ttu-id="073c4-155">Sur hello **Huddle de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="073c4-155">On hello **Huddle Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_url.png)

    <span data-ttu-id="073c4-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`http://<company name>.huddle.com`</span><span class="sxs-lookup"><span data-stu-id="073c4-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<company name>.huddle.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="073c4-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="073c4-158">This value is not real.</span></span> <span data-ttu-id="073c4-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="073c4-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="073c4-160">Contact [équipe de support Client de Huddle](https://huddle.zendesk.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="073c4-160">Contact [Huddle Client support team](https://huddle.zendesk.com) tooget this value.</span></span> 

4. <span data-ttu-id="073c4-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="073c4-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_certificate.png) 

5. <span data-ttu-id="073c4-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="073c4-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-huddle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="073c4-165">Sur hello **Huddle de Configuration** , cliquez sur **configurer Huddle** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="073c4-165">On hello **Huddle Configuration** section, click **Configure Huddle** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="073c4-166">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="073c4-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_configure.png) 
    
7. <span data-ttu-id="073c4-168">tooconfigure l’authentification unique sur Huddle côté, vous devez hello toosend téléchargé **certificat**, **SAML Sign-On URL du Service unique**, et **ID d’entité SAML** trop[Équipe de support Client de huddle](https://huddle.zendesk.com).</span><span class="sxs-lookup"><span data-stu-id="073c4-168">tooconfigure single sign-on on Huddle side, you need toosend hello downloaded  **Certificate**, **SAML Single Sign-On Service URL**, and **SAML Entity ID** too[Huddle Client support team](https://huddle.zendesk.com).</span></span> <span data-ttu-id="073c4-169">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="073c4-169">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>  
   
    >[!NOTE]
    > <span data-ttu-id="073c4-170">L’authentification unique doit toobe activé par l’équipe de support Huddle hello.</span><span class="sxs-lookup"><span data-stu-id="073c4-170">Single sign-on needs toobe enabled by hello Huddle support team.</span></span> <span data-ttu-id="073c4-171">Vous recevez une notification lors de la configuration de hello a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="073c4-171">You get a notification when hello configuration has been completed.</span></span> 
    > 

> [!TIP]
> <span data-ttu-id="073c4-172">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="073c4-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="073c4-173">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="073c4-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="073c4-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="073c4-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 
   
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="073c4-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="073c4-175">Creating an Azure AD test user</span></span>

<span data-ttu-id="073c4-176">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="073c4-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="073c4-178">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="073c4-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="073c4-179">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="073c4-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="073c4-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="073c4-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="073c4-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="073c4-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="073c4-185">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="073c4-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-huddle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="073c4-187">a.</span><span class="sxs-lookup"><span data-stu-id="073c4-187">a.</span></span> <span data-ttu-id="073c4-188">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="073c4-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="073c4-189">b.</span><span class="sxs-lookup"><span data-stu-id="073c4-189">b.</span></span> <span data-ttu-id="073c4-190">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="073c4-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="073c4-191">c.</span><span class="sxs-lookup"><span data-stu-id="073c4-191">c.</span></span> <span data-ttu-id="073c4-192">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="073c4-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="073c4-193">d.</span><span class="sxs-lookup"><span data-stu-id="073c4-193">d.</span></span> <span data-ttu-id="073c4-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="073c4-194">Click **Create**.</span></span>
 
### <a name="creating-a-huddle-test-user"></a><span data-ttu-id="073c4-195">Création d’un utilisateur de test Huddle</span><span class="sxs-lookup"><span data-stu-id="073c4-195">Creating a Huddle test user</span></span>

<span data-ttu-id="073c4-196">tooenable Azure AD les utilisateurs toolog dans tooHuddle, vous devez les configurer dans Huddle.</span><span class="sxs-lookup"><span data-stu-id="073c4-196">tooenable Azure AD users toolog in tooHuddle, they must be provisioned into Huddle.</span></span> <span data-ttu-id="073c4-197">Dans les cas de hello de Huddle, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="073c4-197">In hello case of Huddle, provisioning is a manual task.</span></span>

<span data-ttu-id="073c4-198">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="073c4-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="073c4-199">Connectez-vous à tooyour **Huddle** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="073c4-199">Log in tooyour **Huddle** company site as administrator.</span></span>
2. <span data-ttu-id="073c4-200">Cliquez sur **Workspace**.</span><span class="sxs-lookup"><span data-stu-id="073c4-200">Click **Workspace**.</span></span>
3. <span data-ttu-id="073c4-201">Cliquez sur **People \> Invite People**.</span><span class="sxs-lookup"><span data-stu-id="073c4-201">Click **People \> Invite People**.</span></span>
   
   <span data-ttu-id="073c4-202">![Personnes](./media/active-directory-saas-huddle-tutorial/IC787838.png "Personnes")</span><span class="sxs-lookup"><span data-stu-id="073c4-202">![People](./media/active-directory-saas-huddle-tutorial/IC787838.png "People")</span></span>

4. <span data-ttu-id="073c4-203">Bonjour **créer une nouvelle invitation** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="073c4-203">In hello **Create a new invitation** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="073c4-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span><span class="sxs-lookup"><span data-stu-id="073c4-204">![New Invitation](./media/active-directory-saas-huddle-tutorial/IC787839.png "New Invitation")</span></span>
   
   <span data-ttu-id="073c4-205">a.</span><span class="sxs-lookup"><span data-stu-id="073c4-205">a.</span></span> <span data-ttu-id="073c4-206">Bonjour **choisir un toojoin de personnes équipe tooinvite** liste, sélectionnez **team**.</span><span class="sxs-lookup"><span data-stu-id="073c4-206">In hello **Choose a team tooinvite people toojoin** list, select **team**.</span></span>

   <span data-ttu-id="073c4-207">b.</span><span class="sxs-lookup"><span data-stu-id="073c4-207">b.</span></span> <span data-ttu-id="073c4-208">Hello de type **adresse de messagerie** d’un Azure AD valide compte souhaité tooprovision dans trop**Entrez votre adresse e-mail pour les personnes vous aimeriez tooinvite** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="073c4-208">Type hello **Email Address** of a valid Azure AD account you want tooprovision in too**Enter email address for people you'd like tooinvite** textbox.</span></span>

   <span data-ttu-id="073c4-209">c.</span><span class="sxs-lookup"><span data-stu-id="073c4-209">c.</span></span> <span data-ttu-id="073c4-210">Cliquez sur **Invite**.</span><span class="sxs-lookup"><span data-stu-id="073c4-210">Click **Invite**.</span></span>   
   
    >[!NOTE]
    > <span data-ttu-id="073c4-211">Hello compte Azure AD détenteur recevra un message électronique contenant un compte de hello tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="073c4-211">hello Azure AD account holder will receive an email including a link tooconfirm hello account before it becomes active.</span></span> 
    > 

>[!NOTE]
><span data-ttu-id="073c4-212">Vous pouvez utiliser n’importe quel autre Huddle utilisateur compte outil de création ou API fournie par Huddle tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="073c4-212">You can use any other Huddle user account creation tools or APIs provided by Huddle tooprovision Azure AD user accounts.</span></span> 
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="073c4-213">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="073c4-213">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="073c4-214">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooHuddle.</span><span class="sxs-lookup"><span data-stu-id="073c4-214">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHuddle.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="073c4-216">**tooassign Britta Simon tooHuddle, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="073c4-216">**tooassign Britta Simon tooHuddle, perform hello following steps:**</span></span>

1. <span data-ttu-id="073c4-217">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="073c4-217">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="073c4-219">Dans la liste des applications hello, sélectionnez **Huddle**.</span><span class="sxs-lookup"><span data-stu-id="073c4-219">In hello applications list, select **Huddle**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-huddle-tutorial/tutorial_huddle_app.png) 

3. <span data-ttu-id="073c4-221">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="073c4-221">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="073c4-223">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="073c4-223">Click **Add** button.</span></span> <span data-ttu-id="073c4-224">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="073c4-224">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="073c4-226">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="073c4-226">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="073c4-227">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="073c4-227">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="073c4-228">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="073c4-228">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="073c4-229">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="073c4-229">Testing single sign-on</span></span>

<span data-ttu-id="073c4-230">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="073c4-230">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="073c4-231">Lorsque vous cliquez sur mosaïque Huddle hello hello volet d’accès, vous devez obtenir automatiquement page de connexion de l’application de Huddle.</span><span class="sxs-lookup"><span data-stu-id="073c4-231">When you click hello Huddle tile in hello Access Panel, you should get automatically login page of Huddle application.</span></span>
<span data-ttu-id="073c4-232">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="073c4-232">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="073c4-233">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="073c4-233">Additional resources</span></span>

* [<span data-ttu-id="073c4-234">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="073c4-234">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="073c4-235">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="073c4-235">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_04.png
[100]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_100.png
[200]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-huddle-tutorial/tutorial_general_203.png
