---
title: "Didacticiel : Intégration d’Azure Active Directory à Neota Logic Studio | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Neota logique Studio."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 842605e6-a91d-42cc-a0bb-e23e67173ae2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: jeedes
ms.openlocfilehash: a479ee49618de8275132dbc2c21a8ef723d92d02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-neota-logic-studio"></a><span data-ttu-id="11320-103">Didacticiel : Intégration d’Azure Active Directory à Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="11320-103">Tutorial: Azure Active Directory integration with Neota Logic Studio</span></span>

<span data-ttu-id="11320-104">Dans ce didacticiel, vous apprendrez comment toointegrate Studio logique de Neota avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="11320-104">In this tutorial, you learn how toointegrate Neota Logic Studio with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="11320-105">Intégration Neota logique Studio à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="11320-105">Integrating Neota Logic Studio with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="11320-106">Vous pouvez contrôler dans Azure AD qui a accès tooNeota logique Studio</span><span class="sxs-lookup"><span data-stu-id="11320-106">You can control in Azure AD who has access tooNeota Logic Studio</span></span>
- <span data-ttu-id="11320-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooNeota Studio logique (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="11320-107">You can enable your users tooautomatically get signed-on tooNeota Logic Studio (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="11320-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="11320-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="11320-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez.</span><span class="sxs-lookup"><span data-stu-id="11320-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="11320-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="11320-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11320-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="11320-111">Prerequisites</span></span>

<span data-ttu-id="11320-112">tooconfigure intégration d’Azure AD avec Neota logique Studio, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="11320-112">tooconfigure Azure AD integration with Neota Logic Studio, you need hello following items:</span></span>

- <span data-ttu-id="11320-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="11320-113">An Azure AD subscription</span></span>
- <span data-ttu-id="11320-114">Un abonnement Neota Logic Studio pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="11320-114">A Neota Logic Studio single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="11320-115">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="11320-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="11320-116">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="11320-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="11320-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="11320-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="11320-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="11320-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="11320-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="11320-119">Scenario description</span></span>

<span data-ttu-id="11320-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="11320-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="11320-121">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="11320-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="11320-122">Ajout de Neota logique Studio à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="11320-122">Adding Neota Logic Studio from hello gallery</span></span>
2. <span data-ttu-id="11320-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="11320-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-neota-logic-studio-from-hello-gallery"></a><span data-ttu-id="11320-124">Ajout de Neota logique Studio à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="11320-124">Adding Neota Logic Studio from hello gallery</span></span>

<span data-ttu-id="11320-125">intégration de hello tooconfigure de Neota logique Studio dans Azure AD, vous devez tooadd Neota logique Studio à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="11320-125">tooconfigure hello integration of Neota Logic Studio into Azure AD, you need tooadd Neota Logic Studio from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="11320-126">**tooadd Studio logique de Neota à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="11320-126">**tooadd Neota Logic Studio from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="11320-127">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="11320-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="11320-129">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="11320-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="11320-130">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="11320-130">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="11320-132">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="11320-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="11320-134">Dans la zone de recherche de hello, tapez **Neota logique Studio**.</span><span class="sxs-lookup"><span data-stu-id="11320-134">In hello search box, type **Neota Logic Studio**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_search.png)

5. <span data-ttu-id="11320-136">Dans le volet de résultats hello, sélectionnez **Neota logique Studio**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="11320-136">In hello results panel, select **Neota Logic Studio**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="11320-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="11320-138">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="11320-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Neota Logic Studio pour un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="11320-139">In this section, you configure and test Azure AD single sign-on with Neota Logic Studio based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="11320-140">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Neota logique Studio est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11320-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Neota Logic Studio is tooa user in Azure AD.</span></span> <span data-ttu-id="11320-141">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Neota logique Studio doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="11320-141">In other words, a link relationship between an Azure AD user and hello related user in Neota Logic Studio needs toobe established.</span></span>

<span data-ttu-id="11320-142">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Neota logique Studio.</span><span class="sxs-lookup"><span data-stu-id="11320-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Neota Logic Studio.</span></span>

<span data-ttu-id="11320-143">tooconfigure et test Azure AD l’authentification unique avec Neota logique Studio, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="11320-143">tooconfigure and test Azure AD single sign-on with Neota Logic Studio, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="11320-144">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="11320-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="11320-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="11320-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="11320-146">**[Création d’un utilisateur de test Neota logique Studio](#creating-a-neota-logic-studio-test-user)**  -toohave un équivalent de Britta Simon dans Studio logique Neota qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="11320-146">**[Creating a Neota Logic Studio test user](#creating-a-neota-logic-studio-test-user)** - toohave a counterpart of Britta Simon in Neota Logic Studio that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="11320-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="11320-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="11320-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="11320-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="11320-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="11320-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="11320-150">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Neota logique Studio.</span><span class="sxs-lookup"><span data-stu-id="11320-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Neota Logic Studio application.</span></span>

<span data-ttu-id="11320-151">**tooconfigure Azure AD l’authentification unique avec Neota logique Studio, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="11320-151">**tooconfigure Azure AD single sign-on with Neota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="11320-152">Bonjour portail Azure, sur hello **Neota logique Studio** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="11320-152">In hello Azure portal, on hello **Neota Logic Studio** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="11320-154">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="11320-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_samlbase.png)

3. <span data-ttu-id="11320-156">Sur hello **Neota logique Studio domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="11320-156">On hello **Neota Logic Studio Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_url.png)

    <span data-ttu-id="11320-158">a.</span><span class="sxs-lookup"><span data-stu-id="11320-158">a.</span></span> <span data-ttu-id="11320-159">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<sub domain>.neotalogic.com/a/<sub application>`</span><span class="sxs-lookup"><span data-stu-id="11320-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/a/<sub application>`</span></span>

    <span data-ttu-id="11320-160">b.</span><span class="sxs-lookup"><span data-stu-id="11320-160">b.</span></span> <span data-ttu-id="11320-161">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<sub domain>.neotalogic.com/wb`</span><span class="sxs-lookup"><span data-stu-id="11320-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<sub domain>.neotalogic.com/wb`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="11320-162">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="11320-162">These values are not hello real.</span></span> <span data-ttu-id="11320-163">Mettre à jour les valeurs de hello réel URL de connexion & d’identificateur.</span><span class="sxs-lookup"><span data-stu-id="11320-163">Update these values with hello actual Sign-On URL & Identifier.</span></span> <span data-ttu-id="11320-164">Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur.</span><span class="sxs-lookup"><span data-stu-id="11320-164">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="11320-165">Contact [équipe de support Client de Studio logique Neota](https://www.neotalogic.com/contact-us/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="11320-165">Contact [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) tooget these values.</span></span> 
 
4. <span data-ttu-id="11320-166">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="11320-166">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_certificate.png) 

5. <span data-ttu-id="11320-168">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="11320-168">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="11320-170">tooget SSO configuré pour votre application, contactez [prise en charge Neota logique Studio](https://www.neotalogic.com/contact-us/) d’équipe et les fournir avec téléchargé **Metadata XML** fichier.</span><span class="sxs-lookup"><span data-stu-id="11320-170">tooget SSO configured for your application, Contact [Neota Logic Studio support](https://www.neotalogic.com/contact-us/) team and provide them with downloaded **Metadata XML** file.</span></span>

> [!TIP]
> <span data-ttu-id="11320-171">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="11320-171">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="11320-172">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="11320-172">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="11320-173">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="11320-173">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="11320-174">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="11320-174">Creating an Azure AD test user</span></span>
<span data-ttu-id="11320-175">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="11320-175">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="11320-177">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="11320-177">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="11320-178">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="11320-178">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="11320-180">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="11320-180">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="11320-182">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="11320-182">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="11320-184">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="11320-184">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-neotalogicstudio-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="11320-186">a.</span><span class="sxs-lookup"><span data-stu-id="11320-186">a.</span></span> <span data-ttu-id="11320-187">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="11320-187">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="11320-188">b.</span><span class="sxs-lookup"><span data-stu-id="11320-188">b.</span></span> <span data-ttu-id="11320-189">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="11320-189">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="11320-190">c.</span><span class="sxs-lookup"><span data-stu-id="11320-190">c.</span></span> <span data-ttu-id="11320-191">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="11320-191">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="11320-192">d.</span><span class="sxs-lookup"><span data-stu-id="11320-192">d.</span></span> <span data-ttu-id="11320-193">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="11320-193">Click **Create**.</span></span>
 
### <a name="creating-a-neota-logic-studio-test-user"></a><span data-ttu-id="11320-194">Création d’un utilisateur de test Neota Logic Studio</span><span class="sxs-lookup"><span data-stu-id="11320-194">Creating a Neota Logic Studio test user</span></span>

<span data-ttu-id="11320-195">Dans cette section, vous allez créer un utilisateur nommé Britta Simon dans Neota Logic Studio.</span><span class="sxs-lookup"><span data-stu-id="11320-195">In this section, you create a user called Britta Simon in Neota Logic Studio.</span></span> <span data-ttu-id="11320-196">fonctionnent avec [équipe de support Client de Studio logique Neota](https://www.neotalogic.com/contact-us/) pour ajouter des utilisateurs de hello de plateforme de Neota logique Studio hello.</span><span class="sxs-lookup"><span data-stu-id="11320-196">work with [Neota Logic Studio Client support team](https://www.neotalogic.com/contact-us/) to add hello users in hello Neota Logic Studio platform.</span></span> <span data-ttu-id="11320-197">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="11320-197">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="11320-198">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="11320-198">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="11320-199">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooNeota logique Studio.</span><span class="sxs-lookup"><span data-stu-id="11320-199">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooNeota Logic Studio.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="11320-201">**tooassign Britta Simon tooNeota logique Studio, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="11320-201">**tooassign Britta Simon tooNeota Logic Studio, perform hello following steps:**</span></span>

1. <span data-ttu-id="11320-202">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="11320-202">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="11320-204">Dans la liste des applications hello, sélectionnez **Neota logique Studio**.</span><span class="sxs-lookup"><span data-stu-id="11320-204">In hello applications list, select **Neota Logic Studio**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_neotalogicstudio_app.png) 

3. <span data-ttu-id="11320-206">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="11320-206">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="11320-208">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="11320-208">Click **Add** button.</span></span> <span data-ttu-id="11320-209">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="11320-209">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="11320-211">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="11320-211">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="11320-212">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="11320-212">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="11320-213">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="11320-213">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="11320-214">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="11320-214">Testing single sign-on</span></span>

<span data-ttu-id="11320-215">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="11320-215">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="11320-216">Cliquez sur la vignette de Neota logique Studio hello Bonjour volet d’accès, vous serez redirigé tooOrganization l’authentification sur la page.</span><span class="sxs-lookup"><span data-stu-id="11320-216">Click hello Neota Logic Studio tile in hello Access Panel, you will be redirected tooOrganization sign-on page.</span></span> <span data-ttu-id="11320-217">Connexion réussie, vous serez connecté tooyour application Neota logique Studio.</span><span class="sxs-lookup"><span data-stu-id="11320-217">After successful login, you will be signed-on tooyour Neota Logic Studio application.</span></span> <span data-ttu-id="11320-218">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="11320-218">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span>

<span data-ttu-id="11320-219">Pour plus d’informations sur hello volet d’accès, consultez [présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="11320-219">For more information about hello Access Panel, see [introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="11320-220">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="11320-220">Additional resources</span></span>

* [<span data-ttu-id="11320-221">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="11320-221">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="11320-222">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="11320-222">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-neotalogicstudio-tutorial/tutorial_general_203.png

