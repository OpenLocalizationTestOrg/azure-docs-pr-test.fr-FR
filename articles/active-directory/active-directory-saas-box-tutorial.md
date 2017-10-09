---
title: "Tutorial: Intégration d'Azure Active Directory à Box | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de zone."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5f3517f8-30f2-4be7-9e47-43d702701797
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: jeedes
ms.openlocfilehash: e13a7979761a0b30ecdaac242f1f57a7f8da54c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-box"></a><span data-ttu-id="e2236-103">Didacticiel : Intégration d'Azure Active Directory à Box</span><span class="sxs-lookup"><span data-stu-id="e2236-103">Tutorial: Azure Active Directory integration with Box</span></span>

<span data-ttu-id="e2236-104">Dans ce didacticiel, vous apprendrez comment toointegrate zone avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="e2236-104">In this tutorial, you learn how toointegrate Box with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="e2236-105">Intégration de zone avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="e2236-105">Integrating Box with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="e2236-106">Vous pouvez contrôler dans Azure AD qui a accès tooBox</span><span class="sxs-lookup"><span data-stu-id="e2236-106">You can control in Azure AD who has access tooBox</span></span>
- <span data-ttu-id="e2236-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBox (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2236-107">You can enable your users tooautomatically get signed-on tooBox (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="e2236-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="e2236-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="e2236-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="e2236-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2236-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="e2236-110">Prerequisites</span></span>

<span data-ttu-id="e2236-111">tooconfigure intégration d’Azure AD à Box, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="e2236-111">tooconfigure Azure AD integration with Box, you need hello following items:</span></span>

- <span data-ttu-id="e2236-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2236-112">An Azure AD subscription</span></span>
- <span data-ttu-id="e2236-113">Un abonnement Box pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="e2236-113">A Box single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="e2236-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e2236-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="e2236-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="e2236-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="e2236-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e2236-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="e2236-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e2236-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="e2236-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="e2236-118">Scenario description</span></span>
<span data-ttu-id="e2236-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="e2236-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="e2236-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="e2236-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="e2236-121">Ajout de zone à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e2236-121">Adding Box from hello gallery</span></span>
2. <span data-ttu-id="e2236-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2236-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-box-from-hello-gallery"></a><span data-ttu-id="e2236-123">Ajout de zone à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="e2236-123">Adding Box from hello gallery</span></span>
<span data-ttu-id="e2236-124">intégration de hello tooconfigure de boîte dans Azure AD, vous devez tooadd zone de liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="e2236-124">tooconfigure hello integration of Box into Azure AD, you need tooadd Box from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="e2236-125">**tooadd zone à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e2236-125">**tooadd Box from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2236-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e2236-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="e2236-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e2236-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="e2236-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e2236-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="e2236-131">Cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="e2236-131">Click **New application** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="e2236-133">Dans la zone de recherche de hello, tapez **boîte**.</span><span class="sxs-lookup"><span data-stu-id="e2236-133">In hello search box, type **Box**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_search.png)

5. <span data-ttu-id="e2236-135">Dans le volet de résultats hello, sélectionnez **zone**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="e2236-135">In hello results panel, select **Box**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-box-tutorial/tutorial_box_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="e2236-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2236-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="e2236-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Box, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="e2236-138">In this section, you configure and test Azure AD single sign-on with Box based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="e2236-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans la zone est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e2236-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Box is tooa user in Azure AD.</span></span> <span data-ttu-id="e2236-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans la zone doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="e2236-140">In other words, a link relationship between an Azure AD user and hello related user in Box needs toobe established.</span></span>

<span data-ttu-id="e2236-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans la zone.</span><span class="sxs-lookup"><span data-stu-id="e2236-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Box.</span></span>

<span data-ttu-id="e2236-142">tooconfigure et test Azure AD l’authentification unique avec une zone, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="e2236-142">tooconfigure and test Azure AD single sign-on with Box, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="e2236-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="e2236-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="e2236-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="e2236-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="e2236-145">**[Création d’un utilisateur de test boîte](#creating-a-box-test-user)**  -toohave un équivalent de Britta Simon dans la zone qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e2236-145">**[Creating a Box test user](#creating-a-box-test-user)** - toohave a counterpart of Britta Simon in Box that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="e2236-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e2236-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="e2236-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="e2236-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="e2236-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2236-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="e2236-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de zone.</span><span class="sxs-lookup"><span data-stu-id="e2236-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Box application.</span></span>

<span data-ttu-id="e2236-150">**tooconfigure Azure AD-authentification par zone, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e2236-150">**tooconfigure Azure AD single sign-on with Box, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2236-151">Bonjour portail Azure, sur hello **zone** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="e2236-151">In hello Azure portal, on hello **Box** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="e2236-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="e2236-153">On hello **Single sign-on** dialog, select **Mode** as **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-box-tutorial/tutorial_box_samlbase.png)

3. <span data-ttu-id="e2236-155">Sur hello **zone de domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e2236-155">On hello **Box Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-box-tutorial/tutorial_box_url.png)

    <span data-ttu-id="e2236-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.box.com`</span><span class="sxs-lookup"><span data-stu-id="e2236-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.box.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="e2236-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="e2236-158">This value is not real.</span></span> <span data-ttu-id="e2236-159">Mettre à jour la valeur de hello avec l’URL de connexion réel hello.</span><span class="sxs-lookup"><span data-stu-id="e2236-159">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="e2236-160">Contact [équipe de support Client de la zone](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="e2236-160">Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) tooget this value.</span></span> 
 
4. <span data-ttu-id="e2236-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="e2236-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-box-tutorial/tutorial_box_certificate.png) 

5. <span data-ttu-id="e2236-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="e2236-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-box-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="e2236-165">tooget SSO configuré pour votre application, contactez [équipe de support Client de la zone](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) et leur fournir un fichier XML de hello téléchargé.</span><span class="sxs-lookup"><span data-stu-id="e2236-165">tooget SSO configured for your application, Contact [Box Client support team](https://community.box.com/t5/custom/page/page-id/submit_sso_questionaire) and provide them with hello downloaded XML file.</span></span>

> [!TIP]
> <span data-ttu-id="e2236-166">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="e2236-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="e2236-167">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="e2236-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="e2236-168">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="e2236-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="e2236-169">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2236-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="e2236-170">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="e2236-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="e2236-172">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e2236-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2236-173">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="e2236-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="e2236-175">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e2236-175">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="e2236-177">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="e2236-177">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="e2236-179">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="e2236-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-box-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="e2236-181">a.</span><span class="sxs-lookup"><span data-stu-id="e2236-181">a.</span></span> <span data-ttu-id="e2236-182">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="e2236-182">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="e2236-183">b.</span><span class="sxs-lookup"><span data-stu-id="e2236-183">b.</span></span> <span data-ttu-id="e2236-184">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="e2236-184">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="e2236-185">c.</span><span class="sxs-lookup"><span data-stu-id="e2236-185">c.</span></span> <span data-ttu-id="e2236-186">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="e2236-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="e2236-187">d.</span><span class="sxs-lookup"><span data-stu-id="e2236-187">d.</span></span> <span data-ttu-id="e2236-188">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="e2236-188">Click **Create**.</span></span>
 
### <a name="creating-a-box-test-user"></a><span data-ttu-id="e2236-189">Création d’un utilisateur de test Box</span><span class="sxs-lookup"><span data-stu-id="e2236-189">Creating a Box test user</span></span>

<span data-ttu-id="e2236-190">Dans cette section, un utilisateur appelé Britta Simon est créé dans Box.</span><span class="sxs-lookup"><span data-stu-id="e2236-190">In this section, a user called Britta Simon is created in Box.</span></span> <span data-ttu-id="e2236-191">Box prend en charge l’approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="e2236-191">Box supports just-in-time provisioning, which is enabled by default.</span></span>
<span data-ttu-id="e2236-192">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="e2236-192">There is no action item for you in this section.</span></span> <span data-ttu-id="e2236-193">Si un utilisateur n’existe pas déjà dans la zone, un nouveau est créé lorsque vous essayez de tooaccess boîte.</span><span class="sxs-lookup"><span data-stu-id="e2236-193">If a user doesn't already exist in Box, a new one is created when you attempt tooaccess Box.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="e2236-194">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="e2236-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="e2236-195">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooBox.</span><span class="sxs-lookup"><span data-stu-id="e2236-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooBox.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="e2236-197">**tooassign Britta Simon tooBox, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="e2236-197">**tooassign Britta Simon tooBox, perform hello following steps:**</span></span>

1. <span data-ttu-id="e2236-198">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="e2236-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="e2236-200">Dans la liste des applications hello, sélectionnez **boîte**.</span><span class="sxs-lookup"><span data-stu-id="e2236-200">In hello applications list, select **Box**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-box-tutorial/tutorial_box_app.png) 

3. <span data-ttu-id="e2236-202">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e2236-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="e2236-204">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="e2236-204">Click **Add** button.</span></span> <span data-ttu-id="e2236-205">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e2236-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="e2236-207">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="e2236-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="e2236-208">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e2236-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="e2236-209">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="e2236-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="e2236-210">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="e2236-210">Testing single sign-on</span></span>

<span data-ttu-id="e2236-211">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="e2236-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="e2236-212">Lorsque vous cliquez sur mosaïque de zone hello Bonjour volet d’accès, vous devez obtenir login page tooget connecté tooyour application de zone.</span><span class="sxs-lookup"><span data-stu-id="e2236-212">When you click hello Box tile in hello Access Panel, you should get login page tooget signed-on tooyour Box application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e2236-213">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e2236-213">Additional resources</span></span>

* [<span data-ttu-id="e2236-214">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e2236-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="e2236-215">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="e2236-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="e2236-216">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="e2236-216">Configure User Provisioning</span></span>](active-directory-saas-box-userprovisioning-tutorial.md)


<!--Image references-->

[1]: ./media/active-directory-saas-box-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-box-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-box-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-box-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-box-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-box-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-box-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-box-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-box-tutorial/tutorial_general_203.png

