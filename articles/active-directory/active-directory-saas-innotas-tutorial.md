---
title: "Didacticiel : Intégration d’Azure Active Directory avec Innotas | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Innotas."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: eb9e9c2c-4b09-4177-bbab-423fd657448e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: jeedes
ms.openlocfilehash: 31d787a351fe9362e35afee28a292c927f43702d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-innotas"></a><span data-ttu-id="232ad-103">Didacticiel : Intégration d’Azure Active Directory à Innotas</span><span class="sxs-lookup"><span data-stu-id="232ad-103">Tutorial: Azure Active Directory integration with Innotas</span></span>

<span data-ttu-id="232ad-104">Dans ce didacticiel, vous apprendrez comment toointegrate Innotas avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="232ad-104">In this tutorial, you learn how toointegrate Innotas with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="232ad-105">Intégration d’Innotas à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="232ad-105">Integrating Innotas with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="232ad-106">Vous pouvez contrôler dans Azure AD qui a accès tooInnotas</span><span class="sxs-lookup"><span data-stu-id="232ad-106">You can control in Azure AD who has access tooInnotas</span></span>
- <span data-ttu-id="232ad-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooInnotas (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="232ad-107">You can enable your users tooautomatically get signed-on tooInnotas (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="232ad-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="232ad-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="232ad-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="232ad-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="232ad-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="232ad-110">Prerequisites</span></span>

<span data-ttu-id="232ad-111">tooconfigure intégration d’Azure AD à Innotas, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="232ad-111">tooconfigure Azure AD integration with Innotas, you need hello following items:</span></span>

- <span data-ttu-id="232ad-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="232ad-112">An Azure AD subscription</span></span>
- <span data-ttu-id="232ad-113">Un abonnement Innotas pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="232ad-113">An Innotas single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="232ad-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="232ad-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="232ad-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="232ad-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="232ad-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="232ad-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="232ad-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="232ad-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="232ad-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="232ad-118">Scenario description</span></span>

<span data-ttu-id="232ad-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="232ad-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="232ad-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="232ad-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="232ad-121">Ajout d’Innotas à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="232ad-121">Adding Innotas from hello gallery</span></span>
2. <span data-ttu-id="232ad-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="232ad-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-innotas-from-hello-gallery"></a><span data-ttu-id="232ad-123">Ajout d’Innotas à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="232ad-123">Adding Innotas from hello gallery</span></span>
<span data-ttu-id="232ad-124">intégration de hello tooconfigure de Innotas dans Azure AD, vous devez tooadd Innotas à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="232ad-124">tooconfigure hello integration of Innotas into Azure AD, you need tooadd Innotas from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="232ad-125">**tooadd Innotas à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="232ad-125">**tooadd Innotas from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="232ad-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="232ad-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="232ad-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="232ad-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="232ad-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="232ad-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="232ad-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="232ad-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="232ad-133">Dans la zone de recherche de hello, tapez **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="232ad-133">In hello search box, type **Innotas**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_search.png)

5. <span data-ttu-id="232ad-135">Dans le volet de résultats hello, sélectionnez **Innotas**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="232ad-135">In hello results panel, select **Innotas**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="232ad-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="232ad-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="232ad-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Innotas avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="232ad-138">In this section, you configure and test Azure AD single sign-on with Innotas based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="232ad-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Innotas est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="232ad-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Innotas is tooa user in Azure AD.</span></span> <span data-ttu-id="232ad-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Innotas doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="232ad-140">In other words, a link relationship between an Azure AD user and hello related user in Innotas needs toobe established.</span></span>

<span data-ttu-id="232ad-141">Dans Innotas, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="232ad-141">In Innotas, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="232ad-142">tooconfigure et test Azure AD l’authentification unique à Innotas, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="232ad-142">tooconfigure and test Azure AD single sign-on with Innotas, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="232ad-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="232ad-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="232ad-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="232ad-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="232ad-145">**[Création d’un utilisateur de test Innotas](#creating-an-innotas-test-user)**  -toohave un équivalent de Britta Simon dans Innotas est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="232ad-145">**[Creating an Innotas test user](#creating-an-innotas-test-user)** - toohave a counterpart of Britta Simon in Innotas that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="232ad-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="232ad-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="232ad-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="232ad-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="232ad-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="232ad-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="232ad-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Innotas.</span><span class="sxs-lookup"><span data-stu-id="232ad-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Innotas application.</span></span>

<span data-ttu-id="232ad-150">**tooconfigure Azure AD single sign-on avec Innotas, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="232ad-150">**tooconfigure Azure AD single sign-on with Innotas, perform hello following steps:**</span></span>

1. <span data-ttu-id="232ad-151">Bonjour portail Azure, sur hello **Innotas** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="232ad-151">In hello Azure portal, on hello **Innotas** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="232ad-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="232ad-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_samlbase.png)

3. <span data-ttu-id="232ad-155">Sur hello **Innotas domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="232ad-155">On hello **Innotas Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_url.png)

    <span data-ttu-id="232ad-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.Innotas.com`</span><span class="sxs-lookup"><span data-stu-id="232ad-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.Innotas.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="232ad-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="232ad-158">This value is not real.</span></span> <span data-ttu-id="232ad-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="232ad-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="232ad-160">Contact [équipe de support technique Innotas Client](https://www.innotas.com/contact) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="232ad-160">Contact [Innotas Client support team](https://www.innotas.com/contact) tooget this value.</span></span> 
 
4. <span data-ttu-id="232ad-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="232ad-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_certificate.png) 

5. <span data-ttu-id="232ad-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="232ad-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-innotas-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="232ad-165">tooconfigure l’authentification unique sur **Innotas** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support technique Innotas](https://www.innotas.com/contact).</span><span class="sxs-lookup"><span data-stu-id="232ad-165">tooconfigure single sign-on on **Innotas** side, you need toosend hello downloaded **Metadata XML** too[Innotas support team](https://www.innotas.com/contact).</span></span> <span data-ttu-id="232ad-166">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="232ad-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="232ad-167">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="232ad-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="232ad-168">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="232ad-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="232ad-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="232ad-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="232ad-170">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="232ad-170">Creating an Azure AD test user</span></span>

<span data-ttu-id="232ad-171">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="232ad-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="232ad-173">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="232ad-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="232ad-174">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="232ad-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="232ad-176">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="232ad-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="232ad-178">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="232ad-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="232ad-180">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="232ad-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-innotas-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="232ad-182">a.</span><span class="sxs-lookup"><span data-stu-id="232ad-182">a.</span></span> <span data-ttu-id="232ad-183">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="232ad-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="232ad-184">b.</span><span class="sxs-lookup"><span data-stu-id="232ad-184">b.</span></span> <span data-ttu-id="232ad-185">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="232ad-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="232ad-186">c.</span><span class="sxs-lookup"><span data-stu-id="232ad-186">c.</span></span> <span data-ttu-id="232ad-187">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="232ad-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="232ad-188">d.</span><span class="sxs-lookup"><span data-stu-id="232ad-188">d.</span></span> <span data-ttu-id="232ad-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="232ad-189">Click **Create**.</span></span>
 
### <a name="creating-an-innotas-test-user"></a><span data-ttu-id="232ad-190">Création d’un utilisateur de test Innotas</span><span class="sxs-lookup"><span data-stu-id="232ad-190">Creating an Innotas test user</span></span>

<span data-ttu-id="232ad-191">Il n’existe aucun élément d’action pour vous tooconfigure configuration de l’utilisateur tooInnotas.</span><span class="sxs-lookup"><span data-stu-id="232ad-191">There is no action item for you tooconfigure user provisioning tooInnotas.</span></span>  
<span data-ttu-id="232ad-192">Quand un utilisateur affecté tente de toolog dans tooInnotas à l’aide du volet d’accès hello, Innotas vérifie l’existence d’un utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="232ad-192">When an assigned user tries toolog in tooInnotas using hello access panel, Innotas checks whether hello user exists.</span></span>  

>[!NOTE]
><span data-ttu-id="232ad-193">Si aucun compte d’utilisateur n’est disponible, Innotas le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="232ad-193">If there is no user account available yet, it is automatically created by Innotas.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="232ad-194">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="232ad-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="232ad-195">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooInnotas.</span><span class="sxs-lookup"><span data-stu-id="232ad-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooInnotas.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="232ad-197">**tooassign Britta Simon tooInnotas, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="232ad-197">**tooassign Britta Simon tooInnotas, perform hello following steps:**</span></span>

1. <span data-ttu-id="232ad-198">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="232ad-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="232ad-200">Dans la liste des applications hello, sélectionnez **Innotas**.</span><span class="sxs-lookup"><span data-stu-id="232ad-200">In hello applications list, select **Innotas**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-innotas-tutorial/tutorial_innotas_app.png) 

3. <span data-ttu-id="232ad-202">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="232ad-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="232ad-204">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="232ad-204">Click **Add** button.</span></span> <span data-ttu-id="232ad-205">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="232ad-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="232ad-207">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="232ad-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="232ad-208">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="232ad-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="232ad-209">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="232ad-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="232ad-210">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="232ad-210">Testing single sign-on</span></span>

<span data-ttu-id="232ad-211">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="232ad-211">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="232ad-212">Lorsque vous cliquez sur hello Innotas vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Innotas application.</span><span class="sxs-lookup"><span data-stu-id="232ad-212">When you click hello Innotas tile in hello Access Panel, you should get automatically signed-on tooyour Innotas application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="232ad-213">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="232ad-213">Additional resources</span></span>

* [<span data-ttu-id="232ad-214">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="232ad-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="232ad-215">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="232ad-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-innotas-tutorial/tutorial_general_203.png

