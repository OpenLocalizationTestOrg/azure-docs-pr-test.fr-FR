---
title: "Didacticiel : Intégration d’Azure Active Directory avec FileCloud | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et FileCloud."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f39f0ddd-b504-4562-971f-77b88d1e75fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: fe58d01f02d6ce99ee9e2f83e7dc72c4434e13b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-filecloud"></a><span data-ttu-id="4de48-103">Didacticiel : Intégration d’Azure Active Directory avec FileCloud</span><span class="sxs-lookup"><span data-stu-id="4de48-103">Tutorial: Azure Active Directory integration with FileCloud</span></span>

<span data-ttu-id="4de48-104">Dans ce didacticiel, vous apprendrez comment toointegrate FileCloud avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4de48-104">In this tutorial, you learn how toointegrate FileCloud with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4de48-105">Intégration FileCloud à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4de48-105">Integrating FileCloud with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4de48-106">Vous pouvez contrôler dans Azure AD qui a accès tooFileCloud.</span><span class="sxs-lookup"><span data-stu-id="4de48-106">You can control in Azure AD who has access tooFileCloud.</span></span>
- <span data-ttu-id="4de48-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooFileCloud (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4de48-107">You can enable your users tooautomatically get signed-on tooFileCloud (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="4de48-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4de48-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="4de48-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4de48-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4de48-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4de48-110">Prerequisites</span></span>

<span data-ttu-id="4de48-111">tooconfigure intégration d’Azure AD avec FileCloud, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4de48-111">tooconfigure Azure AD integration with FileCloud, you need hello following items:</span></span>

- <span data-ttu-id="4de48-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4de48-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4de48-113">Un abonnement FileCloud pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4de48-113">A FileCloud single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4de48-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4de48-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4de48-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="4de48-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4de48-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4de48-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4de48-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4de48-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4de48-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4de48-118">Scenario description</span></span>
<span data-ttu-id="4de48-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4de48-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4de48-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="4de48-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4de48-121">Ajout de FileCloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4de48-121">Adding FileCloud from hello gallery</span></span>
2. <span data-ttu-id="4de48-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4de48-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-filecloud-from-hello-gallery"></a><span data-ttu-id="4de48-123">Ajout de FileCloud à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4de48-123">Adding FileCloud from hello gallery</span></span>
<span data-ttu-id="4de48-124">intégration de hello tooconfigure de FileCloud dans Azure AD, vous devez tooadd FileCloud à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4de48-124">tooconfigure hello integration of FileCloud into Azure AD, you need tooadd FileCloud from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4de48-125">**tooadd FileCloud à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4de48-125">**tooadd FileCloud from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4de48-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4de48-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="4de48-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4de48-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4de48-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4de48-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="4de48-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4de48-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="4de48-133">Dans la zone de recherche de hello, tapez **FileCloud**, sélectionnez **FileCloud** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4de48-133">In hello search box, type **FileCloud**, select **FileCloud** from result panel then click **Add** button tooadd hello application.</span></span>

    ![FileCloud dans la liste des résultats hello](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4de48-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4de48-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="4de48-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec FileCloud, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4de48-136">In this section, you configure and test Azure AD single sign-on with FileCloud based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4de48-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans FileCloud est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4de48-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FileCloud is tooa user in Azure AD.</span></span> <span data-ttu-id="4de48-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans FileCloud doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="4de48-138">In other words, a link relationship between an Azure AD user and hello related user in FileCloud needs toobe established.</span></span>

<span data-ttu-id="4de48-139">Dans FileCloud, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="4de48-139">In FileCloud, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4de48-140">tooconfigure et test Azure AD l’authentification unique avec FileCloud, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="4de48-140">tooconfigure and test Azure AD single sign-on with FileCloud, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4de48-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4de48-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4de48-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4de48-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4de48-143">**[Créer un utilisateur de test FileCloud](#create-a-filecloud-test-user)**  -toohave un équivalent de Britta Simon dans FileCloud est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4de48-143">**[Create a FileCloud test user](#create-a-filecloud-test-user)** - toohave a counterpart of Britta Simon in FileCloud that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4de48-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4de48-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4de48-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="4de48-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4de48-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4de48-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4de48-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application FileCloud.</span><span class="sxs-lookup"><span data-stu-id="4de48-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FileCloud application.</span></span>

<span data-ttu-id="4de48-148">**tooconfigure Azure AD single sign-on avec FileCloud, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4de48-148">**tooconfigure Azure AD single sign-on with FileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="4de48-149">Bonjour portail Azure, sur hello **FileCloud** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4de48-149">In hello Azure portal, on hello **FileCloud** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="4de48-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4de48-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_samlbase.png)

3. <span data-ttu-id="4de48-153">Sur hello **FileCloud domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4de48-153">On hello **FileCloud Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_url.png)

    <span data-ttu-id="4de48-155">a.</span><span class="sxs-lookup"><span data-stu-id="4de48-155">a.</span></span> <span data-ttu-id="4de48-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.filecloudhosted.com`</span><span class="sxs-lookup"><span data-stu-id="4de48-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com`</span></span>

    <span data-ttu-id="4de48-157">b.</span><span class="sxs-lookup"><span data-stu-id="4de48-157">b.</span></span> <span data-ttu-id="4de48-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span><span class="sxs-lookup"><span data-stu-id="4de48-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.filecloudhosted.com/simplesaml/module.php/saml/sp/metadata.php/default-sp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4de48-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="4de48-159">These values are not real.</span></span> <span data-ttu-id="4de48-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="4de48-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4de48-161">Contact [équipe de support Client de FileCloud](mailto:support@codelathe.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="4de48-161">Contact [FileCloud Client support team](mailto:support@codelathe.com) tooget these values.</span></span>

4. <span data-ttu-id="4de48-162">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4de48-162">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_certificate.png) 

5. <span data-ttu-id="4de48-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4de48-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-filecloud-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4de48-166">Sur hello **FileCloud Configuration** , cliquez sur **FileCloud de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="4de48-166">On hello **FileCloud Configuration** section, click **Configure FileCloud** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="4de48-167">Hello de copie **ID d’entité SAML** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="4de48-167">Copy hello **SAML Entity ID** from hello **Quick Reference section.**</span></span>

    ![Configuration de FileCloud](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_configure.png) 

7. <span data-ttu-id="4de48-169">Dans une fenêtre de navigateur web, client de FileCloud tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4de48-169">In a different web browser window, sign-on tooyour FileCloud tenant as an administrator.</span></span>

8. <span data-ttu-id="4de48-170">Dans le volet de navigation gauche hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="4de48-170">On hello left navigation pane, click **Settings**.</span></span> 
   
    ![Section Paramètres côté application](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_000.png)

9. <span data-ttu-id="4de48-172">Dans la section Paramètres, cliquez sur l’onglet **SSO**.</span><span class="sxs-lookup"><span data-stu-id="4de48-172">Click **SSO** tab on Settings section.</span></span> 
   
    ![Onglet Authentification unique côté application](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_001.png)

10. <span data-ttu-id="4de48-174">Dans le panneau **Single Sign On (SSO) Settings** (Paramètres d’authentification unique), sélectionnez **SAML** comme **Default SSO Type** (Type d’authentification unique par défaut).</span><span class="sxs-lookup"><span data-stu-id="4de48-174">Select **SAML** as **Default SSO Type** on **Single Sign On (SSO) Settings** panel.</span></span>
   
    ![Volet Paramètres de l’authentification unique côté application](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_002.png)

11. <span data-ttu-id="4de48-176">Coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure en hello **URL de Point de terminaison IdP** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="4de48-176">Paste **SAML Entity ID**, which you have copied from Azure portal into hello **IdP End Point URL** textbox.</span></span>

    ![Zone de texte IDP End Point URL (URL du point de terminaison IdP)](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_003.png)

12. <span data-ttu-id="4de48-178">Ouvrez votre fichier de métadonnées téléchargé dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **métadonnées IdP** zone de texte sur **paramètres SAML** Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="4de48-178">Open your downloaded metadata file in notepad, copy hello content of it into your clipboard, and then paste it toohello **IdP Meta Data** textbox on **SAML Settings** panel.</span></span>

    ![Section IDP Meta Data (Métadonnées IDP) côté application](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_004.png)

13. <span data-ttu-id="4de48-180">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4de48-180">Click **Save** button.</span></span>

> [!TIP]
> <span data-ttu-id="4de48-181">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="4de48-181">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4de48-182">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="4de48-182">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4de48-183">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4de48-183">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4de48-184">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4de48-184">Create an Azure AD test user</span></span>

<span data-ttu-id="4de48-185">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="4de48-185">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="4de48-187">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4de48-187">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4de48-188">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="4de48-188">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-filecloud-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="4de48-190">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4de48-190">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-filecloud-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="4de48-192">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4de48-192">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-filecloud-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="4de48-194">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4de48-194">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-filecloud-tutorial/create_aaduser_04.png)

    <span data-ttu-id="4de48-196">a.</span><span class="sxs-lookup"><span data-stu-id="4de48-196">a.</span></span> <span data-ttu-id="4de48-197">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4de48-197">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4de48-198">b.</span><span class="sxs-lookup"><span data-stu-id="4de48-198">b.</span></span> <span data-ttu-id="4de48-199">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4de48-199">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="4de48-200">c.</span><span class="sxs-lookup"><span data-stu-id="4de48-200">c.</span></span> <span data-ttu-id="4de48-201">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="4de48-201">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="4de48-202">d.</span><span class="sxs-lookup"><span data-stu-id="4de48-202">d.</span></span> <span data-ttu-id="4de48-203">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4de48-203">Click **Create**.</span></span>
 
### <a name="create-a-filecloud-test-user"></a><span data-ttu-id="4de48-204">Créer un utilisateur de test de FileCloud</span><span class="sxs-lookup"><span data-stu-id="4de48-204">Create a FileCloud test user</span></span>

<span data-ttu-id="4de48-205">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans FileCloud.</span><span class="sxs-lookup"><span data-stu-id="4de48-205">hello objective of this section is toocreate a user called Britta Simon in FileCloud.</span></span> <span data-ttu-id="4de48-206">FileCloud prend en charge le déploiement juste-à-temps, qui est l’option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="4de48-206">FileCloud supports just-in-time provisioning, which is by default enabled.</span></span> <span data-ttu-id="4de48-207">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="4de48-207">There is no action item for you in this section.</span></span> <span data-ttu-id="4de48-208">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess FileCloud s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="4de48-208">A new user is created during an attempt tooaccess FileCloud if it doesn't exist yet.</span></span>

>[!NOTE]
><span data-ttu-id="4de48-209">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello [équipe de support Client de FileCloud](mailto:support@codelathe.com).</span><span class="sxs-lookup"><span data-stu-id="4de48-209">If you need toocreate a user manually, you need toocontact hello [FileCloud Client support team](mailto:support@codelathe.com).</span></span> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="4de48-210">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4de48-210">Assign hello Azure AD test user</span></span>

<span data-ttu-id="4de48-211">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooFileCloud.</span><span class="sxs-lookup"><span data-stu-id="4de48-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFileCloud.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="4de48-213">**tooassign Britta Simon tooFileCloud, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4de48-213">**tooassign Britta Simon tooFileCloud, perform hello following steps:**</span></span>

1. <span data-ttu-id="4de48-214">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4de48-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4de48-216">Dans la liste des applications hello, sélectionnez **FileCloud**.</span><span class="sxs-lookup"><span data-stu-id="4de48-216">In hello applications list, select **FileCloud**.</span></span>

    ![lien de FileCloud Hello dans la liste des Applications hello](./media/active-directory-saas-filecloud-tutorial/tutorial_filecloud_app.png)  

3. <span data-ttu-id="4de48-218">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4de48-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="4de48-220">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4de48-220">Click **Add** button.</span></span> <span data-ttu-id="4de48-221">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4de48-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="4de48-223">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="4de48-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4de48-224">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4de48-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4de48-225">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4de48-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4de48-226">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4de48-226">Test single sign-on</span></span>

<span data-ttu-id="4de48-227">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="4de48-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4de48-228">Lorsque vous cliquez sur mosaïque FileCloud hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour FileCloud application.</span><span class="sxs-lookup"><span data-stu-id="4de48-228">When you click hello FileCloud tile in hello Access Panel, you should get automatically signed-on tooyour FileCloud application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4de48-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4de48-229">Additional resources</span></span>

* [<span data-ttu-id="4de48-230">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4de48-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4de48-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4de48-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-filecloud-tutorial/tutorial_general_203.png

