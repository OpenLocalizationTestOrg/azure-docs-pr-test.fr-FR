---
title: "Didacticiel : Intégration d’Azure Active Directory avec Lynda.com | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à Lynda.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f6c92789-8b64-4049-bac9-8cb928398433
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: jeedes
ms.openlocfilehash: fb8d7824e5121da79e9248393b0cbcb0efaffec1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-lyndacom"></a><span data-ttu-id="ef421-103">Didacticiel : Intégration d’Azure Active Directory à Lynda.com</span><span class="sxs-lookup"><span data-stu-id="ef421-103">Tutorial: Azure Active Directory integration with Lynda.com</span></span>

<span data-ttu-id="ef421-104">Dans ce didacticiel, vous apprendrez comment toointegrate Lynda.com avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="ef421-104">In this tutorial, you learn how toointegrate Lynda.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="ef421-105">Intégration de Lynda.com à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="ef421-105">Integrating Lynda.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="ef421-106">Vous pouvez contrôler dans Azure AD qui a accès tooLynda.com</span><span class="sxs-lookup"><span data-stu-id="ef421-106">You can control in Azure AD who has access tooLynda.com</span></span>
- <span data-ttu-id="ef421-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLynda.com (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef421-107">You can enable your users tooautomatically get signed-on tooLynda.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="ef421-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="ef421-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="ef421-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="ef421-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ef421-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ef421-110">Prerequisites</span></span>

<span data-ttu-id="ef421-111">tooconfigure intégration d’Azure AD à Lynda.com, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="ef421-111">tooconfigure Azure AD integration with Lynda.com, you need hello following items:</span></span>

- <span data-ttu-id="ef421-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef421-112">An Azure AD subscription</span></span>
- <span data-ttu-id="ef421-113">Un abonnement Lynda.com pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="ef421-113">A Lynda.com single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="ef421-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="ef421-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="ef421-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="ef421-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="ef421-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="ef421-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="ef421-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ef421-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="ef421-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="ef421-118">Scenario description</span></span>
<span data-ttu-id="ef421-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="ef421-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="ef421-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="ef421-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="ef421-121">Ajout de Lynda.com à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ef421-121">Adding Lynda.com from hello gallery</span></span>
2. <span data-ttu-id="ef421-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef421-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-lyndacom-from-hello-gallery"></a><span data-ttu-id="ef421-123">Ajout de Lynda.com à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="ef421-123">Adding Lynda.com from hello gallery</span></span>
<span data-ttu-id="ef421-124">tooconfigure hello intégration de Lynda.com dans Azure AD, vous devez tooadd Lynda.com à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="ef421-124">tooconfigure hello integration of Lynda.com into Azure AD, you need tooadd Lynda.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="ef421-125">**tooadd Lynda.com à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ef421-125">**tooadd Lynda.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="ef421-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ef421-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="ef421-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="ef421-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="ef421-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ef421-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="ef421-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="ef421-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="ef421-133">Dans la zone de recherche de hello, tapez **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="ef421-133">In hello search box, type **Lynda.com**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_search.png)

5. <span data-ttu-id="ef421-135">Dans le volet de résultats hello, sélectionnez **Lynda.com**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="ef421-135">In hello results panel, select **Lynda.com**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="ef421-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef421-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="ef421-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Lynda.com grâce à un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="ef421-138">In this section, you configure and test Azure AD single sign-on with Lynda.com based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="ef421-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Lynda.com est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ef421-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Lynda.com is tooa user in Azure AD.</span></span> <span data-ttu-id="ef421-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur de Lynda.com hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="ef421-140">In other words, a link relationship between an Azure AD user and hello related user in Lynda.com needs toobe established.</span></span>

<span data-ttu-id="ef421-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="ef421-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Lynda.com.</span></span>

<span data-ttu-id="ef421-142">tooconfigure et test Azure AD l’authentification unique à Lynda.com, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="ef421-142">tooconfigure and test Azure AD single sign-on with Lynda.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="ef421-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="ef421-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="ef421-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="ef421-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="ef421-145">**[Création d’un utilisateur de test Lynda.com](#creating-a-lyndacom-test-user)**  -toohave un équivalent de Britta Simon dans Lynda.com est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ef421-145">**[Creating a Lynda.com test user](#creating-a-lyndacom-test-user)** - toohave a counterpart of Britta Simon in Lynda.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="ef421-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ef421-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="ef421-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="ef421-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="ef421-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef421-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="ef421-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Lynda.com.</span><span class="sxs-lookup"><span data-stu-id="ef421-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Lynda.com application.</span></span>

<span data-ttu-id="ef421-150">**tooconfigure Azure AD single sign-on avec Lynda.com, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ef421-150">**tooconfigure Azure AD single sign-on with Lynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="ef421-151">Bonjour portail Azure, sur hello **Lynda.com** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="ef421-151">In hello Azure portal, on hello **Lynda.com** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="ef421-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="ef421-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_samlbase.png)

3. <span data-ttu-id="ef421-155">Sur hello **Lynda.com domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ef421-155">On hello **Lynda.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_url.png)

    <span data-ttu-id="ef421-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span><span class="sxs-lookup"><span data-stu-id="ef421-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.lynda.com/Shibboleth.sso/InCommon?providerId=<url>&target=<url> `</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ef421-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="ef421-158">This value is not real.</span></span> <span data-ttu-id="ef421-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="ef421-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="ef421-160">Contact [équipe de support Lynda.com Client](https://www.linkedin.com/help/lynda/ask) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="ef421-160">Contact [Lynda.com Client support team](https://www.linkedin.com/help/lynda/ask) tooget these values.</span></span> 
 
4. <span data-ttu-id="ef421-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="ef421-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_certificate.png) 

5. <span data-ttu-id="ef421-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="ef421-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lynda-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="ef421-165">tooconfigure l’authentification unique sur **Lynda.com** côté, vous devez hello toosend téléchargé **Metadata XML** [prise en charge de Lynda.com](https://www.linkedin.com/help/lynda/ask).</span><span class="sxs-lookup"><span data-stu-id="ef421-165">tooconfigure single sign-on on **Lynda.com** side, you need toosend hello downloaded **Metadata XML** [Lynda.com support](https://www.linkedin.com/help/lynda/ask).</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="ef421-166">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef421-166">Creating an Azure AD test user</span></span>
<span data-ttu-id="ef421-167">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="ef421-167">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="ef421-169">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ef421-169">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="ef421-170">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="ef421-170">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="ef421-172">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="ef421-172">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="ef421-174">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="ef421-174">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="ef421-176">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="ef421-176">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-lynda-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="ef421-178">a.</span><span class="sxs-lookup"><span data-stu-id="ef421-178">a.</span></span> <span data-ttu-id="ef421-179">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="ef421-179">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="ef421-180">b.</span><span class="sxs-lookup"><span data-stu-id="ef421-180">b.</span></span> <span data-ttu-id="ef421-181">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="ef421-181">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="ef421-182">c.</span><span class="sxs-lookup"><span data-stu-id="ef421-182">c.</span></span> <span data-ttu-id="ef421-183">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="ef421-183">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="ef421-184">d.</span><span class="sxs-lookup"><span data-stu-id="ef421-184">d.</span></span> <span data-ttu-id="ef421-185">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="ef421-185">Click **Create**.</span></span>
 
### <a name="creating-a-lyndacom-test-user"></a><span data-ttu-id="ef421-186">Créer un utilisateur de test Lynda.com</span><span class="sxs-lookup"><span data-stu-id="ef421-186">Creating a Lynda.com test user</span></span>

<span data-ttu-id="ef421-187">Il n’existe aucun élément d’action pour vous tooconfigure configuration de l’utilisateur tooLynda.com.</span><span class="sxs-lookup"><span data-stu-id="ef421-187">There is no action item for you tooconfigure user provisioning tooLynda.com.</span></span>  
<span data-ttu-id="ef421-188">Quand un utilisateur affecté tente de toolog dans tooLynda.com à l’aide du volet d’accès hello, Lynda.com vérifie l’existence d’un utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="ef421-188">When an assigned user tries toolog in tooLynda.com using hello access panel, Lynda.com checks whether hello user exists.</span></span>  

<span data-ttu-id="ef421-189">Si aucun compte d'utilisateur n’est disponible, Lynda.com le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ef421-189">If there is no user account available yet, it is automatically created by Lynda.com.</span></span>

>[!NOTE]
><span data-ttu-id="ef421-190">Vous pouvez utiliser n’importe quel autre Lynda.com utilisateur compte outil de création ou API fournie par Lynda.com tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="ef421-190">You can use any other Lynda.com user account creation tools or APIs provided by Lynda.com tooprovision AAD user accounts.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="ef421-191">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="ef421-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="ef421-192">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooLynda.com.</span><span class="sxs-lookup"><span data-stu-id="ef421-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooLynda.com.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="ef421-194">**tooassign Britta Simon tooLynda.com, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="ef421-194">**tooassign Britta Simon tooLynda.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="ef421-195">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="ef421-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="ef421-197">Dans la liste des applications hello, sélectionnez **Lynda.com**.</span><span class="sxs-lookup"><span data-stu-id="ef421-197">In hello applications list, select **Lynda.com**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-lynda-tutorial/tutorial_lynda.com_app.png) 

3. <span data-ttu-id="ef421-199">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ef421-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="ef421-201">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ef421-201">Click **Add** button.</span></span> <span data-ttu-id="ef421-202">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ef421-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="ef421-204">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="ef421-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="ef421-205">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="ef421-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="ef421-206">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="ef421-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="ef421-207">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="ef421-207">Testing single sign-on</span></span>

<span data-ttu-id="ef421-208">Si vous souhaitez tester vos paramètres d’authentification unique, ouvrez le volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="ef421-208">If you want to test your single sign-on settings, open the Access Panel.</span></span> <span data-ttu-id="ef421-209">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ef421-209">For more information about the Access Panel, see [Introduction to the Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="ef421-210">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="ef421-210">Additional resources</span></span>

* [<span data-ttu-id="ef421-211">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ef421-211">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="ef421-212">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="ef421-212">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-lynda-tutorial/tutorial_general_203.png

