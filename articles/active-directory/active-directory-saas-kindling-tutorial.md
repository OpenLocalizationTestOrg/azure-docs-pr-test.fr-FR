---
title: "Didacticiel : Intégration d'Azure Active Directory avec Kindling | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et a."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 71229751-74eb-4c2c-abb4-07caa95754c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: 32ad6116c2690aea2060a2dd56e052f233ad7ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kindling"></a><span data-ttu-id="a2968-103">Didacticiel : Intégration d'Azure Active Directory avec Kindling</span><span class="sxs-lookup"><span data-stu-id="a2968-103">Tutorial: Azure Active Directory integration with Kindling</span></span>

<span data-ttu-id="a2968-104">Dans ce didacticiel, vous apprendrez comment toointegrate Kindling avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a2968-104">In this tutorial, you learn how toointegrate Kindling with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a2968-105">Intégration d’a à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a2968-105">Integrating Kindling with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a2968-106">Vous pouvez contrôler dans Azure AD qui a accès tooKindling</span><span class="sxs-lookup"><span data-stu-id="a2968-106">You can control in Azure AD who has access tooKindling</span></span>
- <span data-ttu-id="a2968-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooKindling (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2968-107">You can enable your users tooautomatically get signed-on tooKindling (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a2968-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a2968-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a2968-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez.</span><span class="sxs-lookup"><span data-stu-id="a2968-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="a2968-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="a2968-110">[what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a2968-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a2968-111">Prerequisites</span></span>

<span data-ttu-id="a2968-112">intégration de tooconfigure Azure AD à a, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a2968-112">tooconfigure Azure AD integration with Kindling, you need hello following items:</span></span>

- <span data-ttu-id="a2968-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2968-113">An Azure AD subscription</span></span>
- <span data-ttu-id="a2968-114">Un abonnement Kindling pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a2968-114">A Kindling single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a2968-115">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a2968-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a2968-116">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="a2968-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a2968-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a2968-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a2968-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a2968-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a2968-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a2968-119">Scenario description</span></span>
<span data-ttu-id="a2968-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a2968-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a2968-121">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="a2968-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a2968-122">Ajout d’a à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a2968-122">Adding Kindling from hello gallery</span></span>
2. <span data-ttu-id="a2968-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2968-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kindling-from-hello-gallery"></a><span data-ttu-id="a2968-124">Ajout d’a à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a2968-124">Adding Kindling from hello gallery</span></span>
<span data-ttu-id="a2968-125">intégration de hello tooconfigure d’a dans Azure AD, vous devez tooadd Kindling à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a2968-125">tooconfigure hello integration of Kindling into Azure AD, you need tooadd Kindling from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a2968-126">**tooadd Kindling à partir de la galerie de hello, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a2968-126">**tooadd Kindling from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2968-127">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a2968-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a2968-129">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a2968-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a2968-130">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a2968-130">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a2968-132">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a2968-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a2968-134">Dans la zone de recherche de hello, tapez **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="a2968-134">In hello search box, type **Kindling**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_search.png)

5. <span data-ttu-id="a2968-136">Dans le volet de résultats hello, sélectionnez **Kindling**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a2968-136">In hello results panel, select **Kindling**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a2968-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2968-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a2968-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kindling, grâce à un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a2968-139">In this section, you configure and test Azure AD single sign-on with Kindling based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a2968-140">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans a est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a2968-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kindling is tooa user in Azure AD.</span></span> <span data-ttu-id="a2968-141">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans toobe de besoins a établie.</span><span class="sxs-lookup"><span data-stu-id="a2968-141">In other words, a link relationship between an Azure AD user and hello related user in Kindling needs toobe established.</span></span>

<span data-ttu-id="a2968-142">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans a.</span><span class="sxs-lookup"><span data-stu-id="a2968-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Kindling.</span></span>

<span data-ttu-id="a2968-143">tooconfigure et test Azure AD l’authentification unique avec a, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="a2968-143">tooconfigure and test Azure AD single sign-on with Kindling, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a2968-144">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a2968-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a2968-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a2968-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a2968-146">**[Création d’un utilisateur de test a](#creating-a-kindling-test-user)**  -toohave de Britta Simon contrepartie dans Kindling qui est lié à la représentation sous forme de toohello Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a2968-146">**[Creating a Kindling test user](#creating-a-kindling-test-user)** - toohave a counterpart of Britta Simon in Kindling that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a2968-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a2968-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a2968-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="a2968-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a2968-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2968-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a2968-150">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application a.</span><span class="sxs-lookup"><span data-stu-id="a2968-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kindling application.</span></span>

<span data-ttu-id="a2968-151">**tooconfigure Azure AD l’authentification unique avec a, exécutez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a2968-151">**tooconfigure Azure AD single sign-on with Kindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2968-152">Bonjour portail Azure, sur hello **Kindling** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a2968-152">In hello Azure portal, on hello **Kindling** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a2968-154">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a2968-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_samlbase.png)

3. <span data-ttu-id="a2968-156">Sur hello **Kindling de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a2968-156">On hello **Kindling Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_url.png)

    <span data-ttu-id="a2968-158">a.</span><span class="sxs-lookup"><span data-stu-id="a2968-158">a.</span></span> <span data-ttu-id="a2968-159">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.kindlingapp.com`</span><span class="sxs-lookup"><span data-stu-id="a2968-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com`</span></span>

    <span data-ttu-id="a2968-160">b.</span><span class="sxs-lookup"><span data-stu-id="a2968-160">b.</span></span>  <span data-ttu-id="a2968-161">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span><span class="sxs-lookup"><span data-stu-id="a2968-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<companyname>.kindlingapp.com/saml/module.php/saml/sp/metadata.php/clientIDP`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="a2968-162">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="a2968-162">These values are not hello real.</span></span> <span data-ttu-id="a2968-163">Mettre à jour ces valeurs avec l’URL de connexion réel hello et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="a2968-163">Update these values with hello actual Sign-on URL and Identifier.</span></span> <span data-ttu-id="a2968-164">Contact [équipe de support a](mailto:support@kindlingapp.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="a2968-164">Contact [Kindling support team](mailto:support@kindlingapp.com) tooget these values.</span></span>
 
4. <span data-ttu-id="a2968-165">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a2968-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_certificate.png) 

5. <span data-ttu-id="a2968-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a2968-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kindling-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a2968-169">Sur hello **Kindling de Configuration** , cliquez sur **configurer Kindling** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="a2968-169">On hello **Kindling Configuration** section, click **Configure Kindling** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="a2968-170">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="a2968-170">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_configure.png) 

7. <span data-ttu-id="a2968-172">tooconfigure l’authentification unique sur **Kindling** côté, vous devez hello toosend téléchargé **certificat (Base64)**, **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique**trop[équipe de support a](mailto:support@kindlingapp.com).</span><span class="sxs-lookup"><span data-stu-id="a2968-172">tooconfigure single sign-on on **Kindling** side, you need toosend hello downloaded **Certificate (Base64)**, **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** too[Kindling support team](mailto:support@kindlingapp.com).</span></span>

> [!TIP]
> <span data-ttu-id="a2968-173">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="a2968-173">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a2968-174">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="a2968-174">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a2968-175">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a2968-175">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a2968-176">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2968-176">Creating an Azure AD test user</span></span>
<span data-ttu-id="a2968-177">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="a2968-177">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a2968-179">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a2968-179">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2968-180">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a2968-180">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a2968-182">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a2968-182">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a2968-184">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="a2968-184">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a2968-186">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a2968-186">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kindling-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a2968-188">a.</span><span class="sxs-lookup"><span data-stu-id="a2968-188">a.</span></span> <span data-ttu-id="a2968-189">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a2968-189">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a2968-190">b.</span><span class="sxs-lookup"><span data-stu-id="a2968-190">b.</span></span> <span data-ttu-id="a2968-191">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a2968-191">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a2968-192">c.</span><span class="sxs-lookup"><span data-stu-id="a2968-192">c.</span></span> <span data-ttu-id="a2968-193">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a2968-193">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a2968-194">d.</span><span class="sxs-lookup"><span data-stu-id="a2968-194">d.</span></span> <span data-ttu-id="a2968-195">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="a2968-195">Click **Create**.</span></span>
 
### <a name="creating-a-kindling-test-user"></a><span data-ttu-id="a2968-196">Création d'un utilisateur de test Kindling</span><span class="sxs-lookup"><span data-stu-id="a2968-196">Creating a Kindling test user</span></span>

<span data-ttu-id="a2968-197">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans a.</span><span class="sxs-lookup"><span data-stu-id="a2968-197">hello objective of this section is toocreate a user called Britta Simon in Kindling.</span></span> <span data-ttu-id="a2968-198">Kindling prend en charge l'approvisionnement juste-à-temps.</span><span class="sxs-lookup"><span data-stu-id="a2968-198">Kindling supports just-in-time provisioning.</span></span> <span data-ttu-id="a2968-199">Vous l'avez déjà activé dans [Configuration de l'authentification unique Azure AD](#configuring-azure-ad-single-sign-on).</span><span class="sxs-lookup"><span data-stu-id="a2968-199">You have already enabled it in [Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on).</span></span>

<span data-ttu-id="a2968-200">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="a2968-200">There is no action item for you in this section.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a2968-201">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a2968-201">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a2968-202">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooKindling.</span><span class="sxs-lookup"><span data-stu-id="a2968-202">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKindling.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a2968-204">**tooassign Britta Simon tooKindling, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a2968-204">**tooassign Britta Simon tooKindling, perform hello following steps:**</span></span>

1. <span data-ttu-id="a2968-205">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a2968-205">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a2968-207">Dans la liste des applications hello, sélectionnez **Kindling**.</span><span class="sxs-lookup"><span data-stu-id="a2968-207">In hello applications list, select **Kindling**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kindling-tutorial/tutorial_kindling_app.png) 

3. <span data-ttu-id="a2968-209">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a2968-209">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a2968-211">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a2968-211">Click **Add** button.</span></span> <span data-ttu-id="a2968-212">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a2968-212">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a2968-214">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="a2968-214">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a2968-215">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a2968-215">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a2968-216">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a2968-216">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a2968-217">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a2968-217">Testing single sign-on</span></span>

<span data-ttu-id="a2968-218">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a2968-218">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a2968-219">Lorsque vous cliquez sur mosaïque a hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour a application.</span><span class="sxs-lookup"><span data-stu-id="a2968-219">When you click hello Kindling tile in hello Access Panel, you should get automatically signed-on tooyour Kindling application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a2968-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a2968-220">Additional resources</span></span>

* [<span data-ttu-id="a2968-221">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a2968-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a2968-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a2968-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kindling-tutorial/tutorial_general_203.png

