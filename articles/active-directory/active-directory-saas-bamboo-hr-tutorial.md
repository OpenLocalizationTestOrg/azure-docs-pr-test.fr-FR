---
title: "Didacticiel : Intégration d’Azure Active Directory à BambooHR | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de BambooHR."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f826b5d2-9c64-47df-bbbf-0adf9eb0fa71
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: jeedes
ms.openlocfilehash: f9083f846beb3a4bf4cebbf18b42aba2dfef2472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bamboohr"></a><span data-ttu-id="688be-103">Didacticiel : Intégration d’Azure Active Directory à BambooHR</span><span class="sxs-lookup"><span data-stu-id="688be-103">Tutorial: Azure Active Directory integration with BambooHR</span></span>

<span data-ttu-id="688be-104">Dans ce didacticiel, vous apprendrez comment toointegrate BambooHR avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="688be-104">In this tutorial, you learn how toointegrate BambooHR with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="688be-105">Intégration de BambooHR à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="688be-105">Integrating BambooHR with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="688be-106">Vous pouvez contrôler dans Azure AD qui a accès tooBambooHR</span><span class="sxs-lookup"><span data-stu-id="688be-106">You can control in Azure AD who has access tooBambooHR</span></span>
- <span data-ttu-id="688be-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBambooHR (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="688be-107">You can enable your users tooautomatically get signed-on tooBambooHR (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="688be-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="688be-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="688be-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="688be-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="688be-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="688be-110">Prerequisites</span></span>

<span data-ttu-id="688be-111">tooconfigure intégration d’Azure AD avec BambooHR, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="688be-111">tooconfigure Azure AD integration with BambooHR, you need hello following items:</span></span>

- <span data-ttu-id="688be-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="688be-112">An Azure AD subscription</span></span>
- <span data-ttu-id="688be-113">Un abonnement BambooHR pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="688be-113">A BambooHR single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="688be-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="688be-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="688be-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="688be-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="688be-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="688be-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="688be-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="688be-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="688be-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="688be-118">Scenario description</span></span>
<span data-ttu-id="688be-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="688be-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="688be-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="688be-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="688be-121">Ajout de BambooHR à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="688be-121">Adding BambooHR from hello gallery</span></span>
2. <span data-ttu-id="688be-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="688be-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bamboohr-from-hello-gallery"></a><span data-ttu-id="688be-123">Ajout de BambooHR à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="688be-123">Adding BambooHR from hello gallery</span></span>
<span data-ttu-id="688be-124">intégration de hello tooconfigure de BambooHR dans Azure AD, vous devez tooadd BambooHR à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="688be-124">tooconfigure hello integration of BambooHR into Azure AD, you need tooadd BambooHR from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="688be-125">**tooadd BambooHR à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="688be-125">**tooadd BambooHR from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="688be-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="688be-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="688be-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="688be-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="688be-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="688be-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="688be-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="688be-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="688be-133">Dans la zone de recherche de hello, tapez **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="688be-133">In hello search box, type **BambooHR**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_search.png)

5. <span data-ttu-id="688be-135">Dans le volet de résultats hello, sélectionnez **BambooHR**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="688be-135">In hello results panel, select **BambooHR**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="688be-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="688be-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="688be-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec BambooHR, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="688be-138">In this section, you configure and test Azure AD single sign-on with BambooHR based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="688be-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans BambooHR est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="688be-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in BambooHR is tooa user in Azure AD.</span></span> <span data-ttu-id="688be-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans BambooHR doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="688be-140">In other words, a link relationship between an Azure AD user and hello related user in BambooHR needs toobe established.</span></span>

<span data-ttu-id="688be-141">Dans BambooHR, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="688be-141">In BambooHR, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="688be-142">tooconfigure et test Azure AD l’authentification unique avec BambooHR, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="688be-142">tooconfigure and test Azure AD single sign-on with BambooHR, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="688be-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="688be-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="688be-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="688be-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="688be-145">**[Création d’un utilisateur de test de BambooHR](#creating-a-bamboohr-test-user)**  -toohave un équivalent de Britta Simon dans BambooHR est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="688be-145">**[Creating a BambooHR test user](#creating-a-bamboohr-test-user)** - toohave a counterpart of Britta Simon in BambooHR that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="688be-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="688be-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="688be-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="688be-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="688be-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="688be-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="688be-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application BambooHR.</span><span class="sxs-lookup"><span data-stu-id="688be-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your BambooHR application.</span></span>

<span data-ttu-id="688be-150">**tooconfigure Azure AD single sign-on avec BambooHR, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="688be-150">**tooconfigure Azure AD single sign-on with BambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="688be-151">Bonjour portail Azure, sur hello **BambooHR** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="688be-151">In hello Azure portal, on hello **BambooHR** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="688be-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="688be-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_samlbase.png)

3. <span data-ttu-id="688be-155">Sur hello **BambooHR domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="688be-155">On hello **BambooHR Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_url.png)

    <span data-ttu-id="688be-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company>.bamboohr.com`</span><span class="sxs-lookup"><span data-stu-id="688be-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<company>.bamboohr.com`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="688be-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="688be-158">This value is not real.</span></span> <span data-ttu-id="688be-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="688be-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="688be-160">Contact [équipe de support Client de BambooHR](https://www.bamboohr.com/contact.php) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="688be-160">Contact [BambooHR Client support team](https://www.bamboohr.com/contact.php) tooget this value.</span></span> 
 
4. <span data-ttu-id="688be-161">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="688be-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_certificate.png) 

5. <span data-ttu-id="688be-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="688be-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="688be-165">Sur hello **BambooHR Configuration** , cliquez sur **configurer de BambooHR** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="688be-165">On hello **BambooHR Configuration** section, click **Configure BambooHR** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="688be-166">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="688be-166">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_configure.png) 

6. <span data-ttu-id="688be-168">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise BambooHR en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="688be-168">In a different web browser window, log into your BambooHR company site as an administrator.</span></span>

7. <span data-ttu-id="688be-169">Sur la page d’accueil de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="688be-169">On hello homepage, perform hello following steps:</span></span>
   
    <span data-ttu-id="688be-170">![Authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Authentification unique")</span><span class="sxs-lookup"><span data-stu-id="688be-170">![Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796691.png "Single Sign-On")</span></span>   

    <span data-ttu-id="688be-171">a.</span><span class="sxs-lookup"><span data-stu-id="688be-171">a.</span></span> <span data-ttu-id="688be-172">Cliquez sur **Applications**.</span><span class="sxs-lookup"><span data-stu-id="688be-172">Click **Apps**.</span></span>
   
    <span data-ttu-id="688be-173">b.</span><span class="sxs-lookup"><span data-stu-id="688be-173">b.</span></span> <span data-ttu-id="688be-174">Dans le menu applications hello hello gauche, cliquez sur **Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="688be-174">In hello apps menu on hello left, click **Single Sign-On**.</span></span>
   
    <span data-ttu-id="688be-175">c.</span><span class="sxs-lookup"><span data-stu-id="688be-175">c.</span></span> <span data-ttu-id="688be-176">Cliquez sur **SAML Single Sign-On**.</span><span class="sxs-lookup"><span data-stu-id="688be-176">Click **SAML Single Sign-On**.</span></span>

8. <span data-ttu-id="688be-177">Bonjour **SAML Single Sign-On** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="688be-177">In hello **SAML Single Sign-On** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="688be-178">![Authentification unique SAML](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "Authentification unique SAML")</span><span class="sxs-lookup"><span data-stu-id="688be-178">![SAML Single Sign-On](./media/active-directory-saas-bamboo-hr-tutorial/ic796692.png "SAML Single Sign-On")</span></span>
   
    <span data-ttu-id="688be-179">a.</span><span class="sxs-lookup"><span data-stu-id="688be-179">a.</span></span> <span data-ttu-id="688be-180">Hello de coller **SAML Sign-On URL du Service unique** valeur hello **Url de connexion SSO** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="688be-180">Paste hello **SAML Single Sign-On Service URL** value into hello **SSO Login Url** textbox.</span></span>
      
    <span data-ttu-id="688be-181">b.</span><span class="sxs-lookup"><span data-stu-id="688be-181">b.</span></span> <span data-ttu-id="688be-182">Ouvrez le certificat codé en base 64 est téléchargé à partir du portail Azure dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat X.509** zone de texte</span><span class="sxs-lookup"><span data-stu-id="688be-182">Open base-64 encoded certificate downloaded from Azure portal in notepad, copy hello content of it into your clipboard, and then paste it toohello **X.509 Certificate** textbox</span></span>
   
    <span data-ttu-id="688be-183">c.</span><span class="sxs-lookup"><span data-stu-id="688be-183">c.</span></span> <span data-ttu-id="688be-184">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="688be-184">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="688be-185">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="688be-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="688be-186">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="688be-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="688be-187">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="688be-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="688be-188">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="688be-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="688be-189">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="688be-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="688be-191">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="688be-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="688be-192">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="688be-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="688be-194">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="688be-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="688be-196">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="688be-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="688be-198">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="688be-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bamboo-hr-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="688be-200">a.</span><span class="sxs-lookup"><span data-stu-id="688be-200">a.</span></span> <span data-ttu-id="688be-201">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="688be-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="688be-202">b.</span><span class="sxs-lookup"><span data-stu-id="688be-202">b.</span></span> <span data-ttu-id="688be-203">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="688be-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="688be-204">c.</span><span class="sxs-lookup"><span data-stu-id="688be-204">c.</span></span> <span data-ttu-id="688be-205">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="688be-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="688be-206">d.</span><span class="sxs-lookup"><span data-stu-id="688be-206">d.</span></span> <span data-ttu-id="688be-207">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="688be-207">Click **Create**.</span></span>
 
### <a name="creating-a-bamboohr-test-user"></a><span data-ttu-id="688be-208">Création d’un utilisateur de test BambooHR</span><span class="sxs-lookup"><span data-stu-id="688be-208">Creating a BambooHR test user</span></span>

<span data-ttu-id="688be-209">tooenable Azure AD les utilisateurs toolog dans tooBambooHR, vous devez les configurer dans BambooHR.</span><span class="sxs-lookup"><span data-stu-id="688be-209">tooenable Azure AD users toolog in tooBambooHR, they must be provisioned into BambooHR.</span></span>  

<span data-ttu-id="688be-210">Dans les cas de hello de BambooHR, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="688be-210">In hello case of BambooHR, provisioning is a manual task.</span></span>

<span data-ttu-id="688be-211">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="688be-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="688be-212">Connectez-vous à tooyour **BambooHR** site en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="688be-212">Log in tooyour **BambooHR** site as administrator.</span></span>

2. <span data-ttu-id="688be-213">Dans la barre d’outils de hello en haut de hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="688be-213">In hello toolbar on hello top, click **Settings**.</span></span>
   
    <span data-ttu-id="688be-214">![Paramètre](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Paramètre")</span><span class="sxs-lookup"><span data-stu-id="688be-214">![Setting](./media/active-directory-saas-bamboo-hr-tutorial/ic796694.png "Setting")</span></span>

3. <span data-ttu-id="688be-215">Cliquez sur **Overview**.</span><span class="sxs-lookup"><span data-stu-id="688be-215">Click **Overview**.</span></span>

4. <span data-ttu-id="688be-216">Dans le volet de navigation gauche hello accédez trop**sécurité \> utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="688be-216">In hello left navigation pane, go too**Security \> Users**.</span></span>

5. <span data-ttu-id="688be-217">Nom d’utilisateur de type hello, mot de passe et adresse de messagerie d’un compte AAD valide que vous voulez tooprovision dans hello liés aux zones de texte.</span><span class="sxs-lookup"><span data-stu-id="688be-217">Type hello user name, password, and email address of a valid AAD account you want tooprovision into hello related textboxes.</span></span>

6. <span data-ttu-id="688be-218">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="688be-218">Click **Save**.</span></span>
        
>[!NOTE]
><span data-ttu-id="688be-219">Vous pouvez utiliser n’importe quel autre BambooHR utilisateur compte outil de création ou API fournie par BambooHR tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="688be-219">You can use any other BambooHR user account creation tools or APIs provided by BambooHR tooprovision AAD user accounts.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="688be-220">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="688be-220">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="688be-221">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooBambooHR.</span><span class="sxs-lookup"><span data-stu-id="688be-221">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBambooHR.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="688be-223">**tooassign Britta Simon tooBambooHR, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="688be-223">**tooassign Britta Simon tooBambooHR, perform hello following steps:**</span></span>

1. <span data-ttu-id="688be-224">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="688be-224">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="688be-226">Dans la liste des applications hello, sélectionnez **BambooHR**.</span><span class="sxs-lookup"><span data-stu-id="688be-226">In hello applications list, select **BambooHR**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bamboo-hr-tutorial/tutorial_bamboohr_app.png) 

3. <span data-ttu-id="688be-228">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="688be-228">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="688be-230">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="688be-230">Click **Add** button.</span></span> <span data-ttu-id="688be-231">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="688be-231">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="688be-233">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="688be-233">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="688be-234">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="688be-234">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="688be-235">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="688be-235">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="688be-236">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="688be-236">Testing single sign-on</span></span>

<span data-ttu-id="688be-237">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="688be-237">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="688be-238">Lorsque vous cliquez sur mosaïque BambooHR hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour BambooHR application.</span><span class="sxs-lookup"><span data-stu-id="688be-238">When you click hello BambooHR tile in hello Access Panel, you should get automatically signed-on tooyour BambooHR application.</span></span>
<span data-ttu-id="688be-239">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="688be-239">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="688be-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="688be-240">Additional resources</span></span>

* [<span data-ttu-id="688be-241">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="688be-241">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="688be-242">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="688be-242">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bamboo-hr-tutorial/tutorial_general_203.png

