---
title: "Didacticiel : Intégration d’Azure Active Directory à 23 Video | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et 23 vidéo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5e73dd1d-3995-4a73-b9cf-1b2318d49cb3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: jeedes
ms.openlocfilehash: 3430e4db3cd1114db62233e6699618071a3646ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-23-video"></a><span data-ttu-id="948d1-103">Didacticiel : Intégration d’Azure Active Directory à 23 Video</span><span class="sxs-lookup"><span data-stu-id="948d1-103">Tutorial: Azure Active Directory integration with 23 Video</span></span>

<span data-ttu-id="948d1-104">Dans ce didacticiel, vous apprendrez comment toointegrate 23 vidéo avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="948d1-104">In this tutorial, you learn how toointegrate 23 Video with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="948d1-105">Intégration de 23 vidéo avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="948d1-105">Integrating 23 Video with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="948d1-106">Vous pouvez contrôler dans Azure AD qui a accès too23 vidéo</span><span class="sxs-lookup"><span data-stu-id="948d1-106">You can control in Azure AD who has access too23 Video</span></span>
- <span data-ttu-id="948d1-107">Vous pouvez activer vos utilisateurs tooautomatically obtenir vidéo too23 (Single Sign-On) signé sur avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="948d1-107">You can enable your users tooautomatically get signed-on too23 Video (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="948d1-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="948d1-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="948d1-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="948d1-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="948d1-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="948d1-110">Prerequisites</span></span>

<span data-ttu-id="948d1-111">tooconfigure intégration d’Azure AD avec 23 vidéo, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="948d1-111">tooconfigure Azure AD integration with 23 Video, you need hello following items:</span></span>

- <span data-ttu-id="948d1-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="948d1-112">An Azure AD subscription</span></span>
- <span data-ttu-id="948d1-113">Un abonnement 23 Video pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="948d1-113">A 23 Video single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="948d1-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="948d1-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="948d1-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="948d1-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="948d1-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="948d1-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="948d1-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="948d1-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="948d1-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="948d1-118">Scenario description</span></span>
<span data-ttu-id="948d1-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="948d1-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="948d1-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="948d1-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="948d1-121">Ajout de 23 vidéo à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="948d1-121">Adding 23 Video from hello gallery</span></span>
2. <span data-ttu-id="948d1-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="948d1-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-23-video-from-hello-gallery"></a><span data-ttu-id="948d1-123">Ajout de 23 vidéo à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="948d1-123">Adding 23 Video from hello gallery</span></span>
<span data-ttu-id="948d1-124">intégration de hello tooconfigure de vidéo 23 dans Azure AD, vous devez tooadd 23 vidéo à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="948d1-124">tooconfigure hello integration of 23 Video into Azure AD, you need tooadd 23 Video from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="948d1-125">**effectuer de vidéo à partir de la galerie hello, tooadd 23 hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="948d1-125">**tooadd 23 Video from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="948d1-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="948d1-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="948d1-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="948d1-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="948d1-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="948d1-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="948d1-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="948d1-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="948d1-133">Dans la zone de recherche de hello, tapez **vidéo 23**.</span><span class="sxs-lookup"><span data-stu-id="948d1-133">In hello search box, type **23 Video**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_search.png)

5. <span data-ttu-id="948d1-135">Dans le volet de résultats hello, sélectionnez **vidéo 23**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="948d1-135">In hello results panel, select **23 Video**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-23video-tutorial/tutorial_23video_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="948d1-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="948d1-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="948d1-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec 23 Video, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="948d1-138">In this section, you configure and test Azure AD single sign-on with 23 Video based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="948d1-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans 23 vidéo est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="948d1-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in 23 Video is tooa user in Azure AD.</span></span> <span data-ttu-id="948d1-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello 23 vidéo doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="948d1-140">In other words, a link relationship between an Azure AD user and hello related user in 23 Video needs toobe established.</span></span>

<span data-ttu-id="948d1-141">Dans une vidéo 23, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="948d1-141">In 23 Video, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="948d1-142">tooconfigure et test Azure AD l’authentification unique avec 23 vidéo, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="948d1-142">tooconfigure and test Azure AD single sign-on with 23 Video, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="948d1-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="948d1-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="948d1-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="948d1-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="948d1-145">**[Création d’un utilisateur de test vidéo 23](#creating-a-23-video-test-user)**  -toohave un équivalent de Britta Simon dans 23 vidéo qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="948d1-145">**[Creating a 23 Video test user](#creating-a-23-video-test-user)** - toohave a counterpart of Britta Simon in 23 Video that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="948d1-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="948d1-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="948d1-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="948d1-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="948d1-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="948d1-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="948d1-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application vidéo 23.</span><span class="sxs-lookup"><span data-stu-id="948d1-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your 23 Video application.</span></span>

<span data-ttu-id="948d1-150">**tooconfigure Azure AD single sign-on avec vidéo 23, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="948d1-150">**tooconfigure Azure AD single sign-on with 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="948d1-151">Bonjour portail Azure, sur hello **vidéo 23** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="948d1-151">In hello Azure portal, on hello **23 Video** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="948d1-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="948d1-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-23video-tutorial/tutorial_23video_samlbase.png)

3. <span data-ttu-id="948d1-155">Sur hello **23 URL et le domaine de la vidéo** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="948d1-155">On hello **23 Video Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-23video-tutorial/tutorial_23video_url.png)

    <span data-ttu-id="948d1-157">a.</span><span class="sxs-lookup"><span data-stu-id="948d1-157">a.</span></span> <span data-ttu-id="948d1-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.23video.com`</span><span class="sxs-lookup"><span data-stu-id="948d1-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.23video.com`</span></span>

    <span data-ttu-id="948d1-159">b.</span><span class="sxs-lookup"><span data-stu-id="948d1-159">b.</span></span> <span data-ttu-id="948d1-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://www.23video.com/saml/trust/<uniqueid>`</span><span class="sxs-lookup"><span data-stu-id="948d1-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://www.23video.com/saml/trust/<uniqueid>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="948d1-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="948d1-161">These values are not real.</span></span> <span data-ttu-id="948d1-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="948d1-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="948d1-163">Contact [équipe de support Client de vidéo 23](mailto:support@23company.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="948d1-163">Contact [23 Video Client support team](mailto:support@23company.com) tooget these values.</span></span> 
 
4. <span data-ttu-id="948d1-164">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="948d1-164">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-23video-tutorial/tutorial_23video_certificate.png) 

5. <span data-ttu-id="948d1-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="948d1-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-23video-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="948d1-168">Sur hello **23 vidéo Configuration** , cliquez sur **configurer une vidéo de 23** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="948d1-168">On hello **23 Video Configuration** section, click **Configure 23 Video** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="948d1-169">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="948d1-169">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-23video-tutorial/tutorial_23video_configure.png) 

7. <span data-ttu-id="948d1-171">tooconfigure l’authentification unique sur **vidéo 23** côté, vous devez hello toosend téléchargé **certificat (Base64)**, **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique**trop[équipe de support technique 23 vidéo](mailto:support@23company.com).</span><span class="sxs-lookup"><span data-stu-id="948d1-171">tooconfigure single sign-on on **23 Video** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[23 Video support team](mailto:support@23company.com).</span></span> 


> [!TIP]
> <span data-ttu-id="948d1-172">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="948d1-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="948d1-173">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="948d1-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="948d1-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="948d1-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="948d1-175">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="948d1-175">Creating an Azure AD test user</span></span>
<span data-ttu-id="948d1-176">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="948d1-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="948d1-178">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="948d1-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="948d1-179">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="948d1-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="948d1-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="948d1-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="948d1-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="948d1-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="948d1-185">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="948d1-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-23video-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="948d1-187">a.</span><span class="sxs-lookup"><span data-stu-id="948d1-187">a.</span></span> <span data-ttu-id="948d1-188">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="948d1-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="948d1-189">b.</span><span class="sxs-lookup"><span data-stu-id="948d1-189">b.</span></span> <span data-ttu-id="948d1-190">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="948d1-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="948d1-191">c.</span><span class="sxs-lookup"><span data-stu-id="948d1-191">c.</span></span> <span data-ttu-id="948d1-192">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="948d1-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="948d1-193">d.</span><span class="sxs-lookup"><span data-stu-id="948d1-193">d.</span></span> <span data-ttu-id="948d1-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="948d1-194">Click **Create**.</span></span>
 
### <a name="creating-a-23-video-test-user"></a><span data-ttu-id="948d1-195">Création d’un utilisateur de test 23 Video</span><span class="sxs-lookup"><span data-stu-id="948d1-195">Creating a 23 Video test user</span></span>

<span data-ttu-id="948d1-196">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans 23 vidéo.</span><span class="sxs-lookup"><span data-stu-id="948d1-196">hello objective of this section is toocreate a user called Britta Simon in 23 Video.</span></span>

<span data-ttu-id="948d1-197">**toocreate un utilisateur appelé Britta Simon dans 23 vidéo, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="948d1-197">**toocreate a user called Britta Simon in 23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="948d1-198">Se connecter tooyour 23 site d’entreprise vidéo en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="948d1-198">Sign on tooyour 23 Video company site as administrator.</span></span>

2. <span data-ttu-id="948d1-199">Accédez trop**paramètres**.</span><span class="sxs-lookup"><span data-stu-id="948d1-199">Go too**Settings**.</span></span>
 
3. <span data-ttu-id="948d1-200">Dans la section **Users**, cliquez sur **Configure**.</span><span class="sxs-lookup"><span data-stu-id="948d1-200">In **Users** section, click **Configure**.</span></span>
   
    ![Affecter des utilisateurs][400]

4. <span data-ttu-id="948d1-202">Cliquez sur **Add a new user**.</span><span class="sxs-lookup"><span data-stu-id="948d1-202">Click **Add a new user**.</span></span> 
   
    ![Affecter des utilisateurs][401]

5. <span data-ttu-id="948d1-204">Bonjour **inviter quelqu'un toojoin ce site** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="948d1-204">In hello **Invite someone toojoin this site** section, perform hello following steps:</span></span>
   
    ![Affecter des utilisateurs][402]

    <span data-ttu-id="948d1-206">a.</span><span class="sxs-lookup"><span data-stu-id="948d1-206">a.</span></span> <span data-ttu-id="948d1-207">Bonjour **adresses de messagerie** zone de texte, tapez l’adresse de messagerie Britta Simon dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="948d1-207">In hello **E-mail addresses** textbox, type Britta Simon's email address in Azure AD.</span></span>  
 
    <span data-ttu-id="948d1-208">b.</span><span class="sxs-lookup"><span data-stu-id="948d1-208">b.</span></span> <span data-ttu-id="948d1-209">Cliquez sur **ajouter un utilisateur hello**.</span><span class="sxs-lookup"><span data-stu-id="948d1-209">Click **Add hello user**.</span></span>   

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="948d1-210">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="948d1-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="948d1-211">Dans cette section, vous activez Britta Simon toouse Azure l’authentification unique en accordant l’accès too23 vidéo.</span><span class="sxs-lookup"><span data-stu-id="948d1-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access too23 Video.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="948d1-213">**tooassign Britta Simon too23 vidéo, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="948d1-213">**tooassign Britta Simon too23 Video, perform hello following steps:**</span></span>

1. <span data-ttu-id="948d1-214">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="948d1-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="948d1-216">Dans la liste des applications hello, sélectionnez **vidéo 23**.</span><span class="sxs-lookup"><span data-stu-id="948d1-216">In hello applications list, select **23 Video**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-23video-tutorial/tutorial_23video_app.png) 

3. <span data-ttu-id="948d1-218">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="948d1-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="948d1-220">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="948d1-220">Click **Add** button.</span></span> <span data-ttu-id="948d1-221">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="948d1-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="948d1-223">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="948d1-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="948d1-224">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="948d1-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="948d1-225">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="948d1-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="948d1-226">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="948d1-226">Testing single sign-on</span></span>

<span data-ttu-id="948d1-227">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="948d1-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="948d1-228">Lorsque vous cliquez sur vignette de vidéo hello 23 Bonjour volet d’accès, vous devez obtenir l’application de vidéo automatiquement signé sur tooyour 23.</span><span class="sxs-lookup"><span data-stu-id="948d1-228">When you click hello 23 Video tile in hello Access Panel, you should get automatically signed-on tooyour 23 Video application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="948d1-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="948d1-229">Additional resources</span></span>

* [<span data-ttu-id="948d1-230">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="948d1-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="948d1-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="948d1-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-23video-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-23video-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-23video-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-23video-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-23video-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-23video-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-23video-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-23video-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-23video-tutorial/tutorial_general_203.png

[400]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_10.png
[401]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_11.png
[402]: ./media/active-directory-saas-23video-tutorial/tutorial_23video_12.png
