---
title: "Didacticiel : Intégration d’Azure Active Directory à Overdrive | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de dépassement."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e68cede7-1130-4813-bd55-22a9a6fc6bf5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: jeedes
ms.openlocfilehash: b0aafacdedee25587132fc88ff93829f4367b0af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-overdrive"></a><span data-ttu-id="05a21-103">Didacticiel : Intégration d’Azure Active Directory avec Overdrive</span><span class="sxs-lookup"><span data-stu-id="05a21-103">Tutorial: Azure Active Directory integration with Overdrive</span></span> 

<span data-ttu-id="05a21-104">Dans ce didacticiel, vous apprendrez comment toointegrate dépassement avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="05a21-104">In this tutorial, you learn how toointegrate Overdrive with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="05a21-105">Intégration de Overdrive à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="05a21-105">Integrating Overdrive with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="05a21-106">Vous pouvez contrôler dans Azure AD qui a accès tooOverdrive</span><span class="sxs-lookup"><span data-stu-id="05a21-106">You can control in Azure AD who has access tooOverdrive</span></span> 
- <span data-ttu-id="05a21-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooOverdrive (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a21-107">You can enable your users tooautomatically get signed-on tooOverdrive (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="05a21-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="05a21-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="05a21-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="05a21-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05a21-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="05a21-110">Prerequisites</span></span>

<span data-ttu-id="05a21-111">tooconfigure intégration d’Azure AD avec une surcharge, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="05a21-111">tooconfigure Azure AD integration with Overdrive, you need hello following items:</span></span>

- <span data-ttu-id="05a21-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a21-112">An Azure AD subscription</span></span>
- <span data-ttu-id="05a21-113">Un abonnement Overdrive pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="05a21-113">An Overdrive single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="05a21-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="05a21-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="05a21-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="05a21-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="05a21-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="05a21-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="05a21-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="05a21-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="05a21-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="05a21-118">Scenario description</span></span>
<span data-ttu-id="05a21-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="05a21-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="05a21-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="05a21-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="05a21-121">Ajout de Overdrive à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="05a21-121">Adding Overdrive from hello gallery</span></span>
2. <span data-ttu-id="05a21-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a21-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-overdrive-from-hello-gallery"></a><span data-ttu-id="05a21-123">Ajout de Overdrive à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="05a21-123">Adding Overdrive from hello gallery</span></span>
<span data-ttu-id="05a21-124">intégration de hello tooconfigure de dépassement dans Azure AD, vous devez tooadd Overdrive à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="05a21-124">tooconfigure hello integration of Overdrive into Azure AD, you need tooadd Overdrive from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="05a21-125">**tooadd Overdrive à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="05a21-125">**tooadd Overdrive from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="05a21-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="05a21-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="05a21-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="05a21-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="05a21-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="05a21-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="05a21-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="05a21-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="05a21-133">Dans la zone de recherche de hello, tapez **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="05a21-133">In hello search box, type **Overdrive**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_search.png)

5. <span data-ttu-id="05a21-135">Dans le volet de résultats hello, sélectionnez **Overdrive**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="05a21-135">In hello results panel, select **Overdrive**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="05a21-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a21-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="05a21-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Overdrive, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="05a21-138">In this section, you configure and test Azure AD single sign-on with Overdrive based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="05a21-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Overdrive est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="05a21-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Overdrive is tooa user in Azure AD.</span></span> <span data-ttu-id="05a21-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Overdrive doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="05a21-140">In other words, a link relationship between an Azure AD user and hello related user in Overdrive needs toobe established.</span></span>

<span data-ttu-id="05a21-141">Dans Overdrive, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="05a21-141">In Overdrive, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="05a21-142">tooconfigure et test Azure AD l’authentification unique avec une surcharge, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="05a21-142">tooconfigure and test Azure AD single sign-on with Overdrive, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="05a21-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="05a21-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="05a21-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="05a21-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="05a21-145">**[Création d’un utilisateur de test Overdrive](#creating-an-overdrive-test-user)**  -toohave un équivalent de Britta Simon dans une surcharge qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="05a21-145">**[Creating an Overdrive test user](#creating-an-overdrive-test-user)** - toohave a counterpart of Britta Simon in Overdrive that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="05a21-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="05a21-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="05a21-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="05a21-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="05a21-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a21-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="05a21-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de dépassement.</span><span class="sxs-lookup"><span data-stu-id="05a21-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Overdrive  application.</span></span>

<span data-ttu-id="05a21-150">**tooconfigure Azure AD single sign-on avec Overdrive, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="05a21-150">**tooconfigure Azure AD single sign-on with Overdrive, perform hello following steps:**</span></span>

1. <span data-ttu-id="05a21-151">Bonjour portail Azure, sur hello **Overdrive** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="05a21-151">In hello Azure portal, on hello **Overdrive** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="05a21-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="05a21-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_samlbase.png)

3. <span data-ttu-id="05a21-155">Sur hello **Overdrive domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="05a21-155">On hello **Overdrive Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_url.png)

    <span data-ttu-id="05a21-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`http://<subdomain>.libraryreserve.com`</span><span class="sxs-lookup"><span data-stu-id="05a21-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<subdomain>.libraryreserve.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="05a21-158">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="05a21-158">hello value is not real.</span></span> <span data-ttu-id="05a21-159">Valeur de hello de mise à jour avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="05a21-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="05a21-160">Contact [équipe de support Overdrive Client](https://help.overdrive.com/) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="05a21-160">Contact [Overdrive Client support team](https://help.overdrive.com/) tooget hello value.</span></span> 
 
4. <span data-ttu-id="05a21-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="05a21-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_certificate.png) 

5. <span data-ttu-id="05a21-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="05a21-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="05a21-165">tooconfigure l’authentification unique sur **Overdrive** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support Overdrive](https://help.overdrive.com/).</span><span class="sxs-lookup"><span data-stu-id="05a21-165">tooconfigure single sign-on on **Overdrive** side, you need toosend hello downloaded **Metadata XML** too[Overdrive support team](https://help.overdrive.com/).</span></span> <span data-ttu-id="05a21-166">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="05a21-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="05a21-167">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="05a21-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="05a21-168">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="05a21-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="05a21-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="05a21-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="05a21-170">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a21-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="05a21-171">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="05a21-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="05a21-173">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="05a21-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="05a21-174">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="05a21-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="05a21-176">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="05a21-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="05a21-178">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="05a21-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="05a21-180">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="05a21-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-overdrive-books-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="05a21-182">a.</span><span class="sxs-lookup"><span data-stu-id="05a21-182">a.</span></span> <span data-ttu-id="05a21-183">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="05a21-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="05a21-184">b.</span><span class="sxs-lookup"><span data-stu-id="05a21-184">b.</span></span> <span data-ttu-id="05a21-185">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="05a21-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="05a21-186">c.</span><span class="sxs-lookup"><span data-stu-id="05a21-186">c.</span></span> <span data-ttu-id="05a21-187">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="05a21-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="05a21-188">d.</span><span class="sxs-lookup"><span data-stu-id="05a21-188">d.</span></span> <span data-ttu-id="05a21-189">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="05a21-189">Click **Create**.</span></span>
 
### <a name="creating-an-overdrive-test-user"></a><span data-ttu-id="05a21-190">Création d’un utilisateur de test Overdrive</span><span class="sxs-lookup"><span data-stu-id="05a21-190">Creating an Overdrive test user</span></span>

<span data-ttu-id="05a21-191">Il n’existe aucun élément d’action pour vous tooconfigure configuration de l’utilisateur tooOverDrive.</span><span class="sxs-lookup"><span data-stu-id="05a21-191">There is no action item for you tooconfigure user provisioning tooOverDrive.</span></span>  

<span data-ttu-id="05a21-192">Lorsqu’un toolog tentatives utilisateur affecté dans tooOverDrive, un compte OverDrive est créé automatiquement si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="05a21-192">When an assigned user tries toolog in tooOverDrive, an OverDrive account is automatically created if necessary.</span></span>

>[!NOTE]
><span data-ttu-id="05a21-193">Vous pouvez utiliser n’importe quel autre OverDrive utilisateur compte outil de création ou API fournie par OverDrive tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="05a21-193">You can use any other OverDrive user account creation tools or APIs provided by OverDrive tooprovision AAD user accounts.</span></span>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="05a21-194">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="05a21-194">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="05a21-195">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooOverdrive.</span><span class="sxs-lookup"><span data-stu-id="05a21-195">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooOverdrive.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="05a21-197">**tooassign Britta Simon tooOverdrive, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="05a21-197">**tooassign Britta Simon tooOverdrive, perform hello following steps:**</span></span>

1. <span data-ttu-id="05a21-198">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="05a21-198">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="05a21-200">Dans la liste des applications hello, sélectionnez **Overdrive**.</span><span class="sxs-lookup"><span data-stu-id="05a21-200">In hello applications list, select **Overdrive**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-overdrive-books-tutorial/tutorial_overdrivebooks_app.png) 

3. <span data-ttu-id="05a21-202">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="05a21-202">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="05a21-204">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="05a21-204">Click **Add** button.</span></span> <span data-ttu-id="05a21-205">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="05a21-205">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="05a21-207">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="05a21-207">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="05a21-208">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="05a21-208">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="05a21-209">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="05a21-209">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="05a21-210">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="05a21-210">Testing single sign-on</span></span>

<span data-ttu-id="05a21-211">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="05a21-211">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="05a21-212">Lorsque vous cliquez sur mosaïque Overdrive hello hello volet d’accès, vous devez obtenir l’application de Overdrive automatiquement signé sur tooyour.</span><span class="sxs-lookup"><span data-stu-id="05a21-212">When you click hello Overdrive tile in hello Access Panel, you should get automatically signed-on tooyour Overdrive application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="05a21-213">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="05a21-213">Additional resources</span></span>

* [<span data-ttu-id="05a21-214">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="05a21-214">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="05a21-215">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="05a21-215">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-overdrive-books-tutorial/tutorial_general_203.png

