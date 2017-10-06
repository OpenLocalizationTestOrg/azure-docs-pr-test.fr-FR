---
title: "Didacticiel : Intégration d’Azure Active Directory à Evidence.com | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Evidence.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: f9a7cb7c-ff67-40dc-872c-1fa35f9dd03b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: jeedes
ms.openlocfilehash: eed98c15dca8a6a77f0b5d407bb40ee0037fccad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-evidencecom"></a><span data-ttu-id="10ac2-103">Didacticiel : Intégration d’Azure Active Directory à Evidence.com</span><span class="sxs-lookup"><span data-stu-id="10ac2-103">Tutorial: Azure Active Directory integration with Evidence.com</span></span>

<span data-ttu-id="10ac2-104">Dans ce didacticiel, vous apprendrez comment toointegrate Evidence.com avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="10ac2-104">In this tutorial, you learn how toointegrate Evidence.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="10ac2-105">Intégration Evidence.com à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="10ac2-105">Integrating Evidence.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="10ac2-106">Vous pouvez contrôler dans Azure AD qui a accès tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="10ac2-106">You can control in Azure AD who has access tooEvidence.com.</span></span>
- <span data-ttu-id="10ac2-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooEvidence.com (Single Sign-On) avec leurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10ac2-107">You can enable your users tooautomatically get signed-on tooEvidence.com (Single Sign-On) with their Azure AD accounts.</span></span>
- <span data-ttu-id="10ac2-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="10ac2-108">You can manage your accounts in one central location - hello Azure portal.</span></span>

<span data-ttu-id="10ac2-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="10ac2-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10ac2-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="10ac2-110">Prerequisites</span></span>

<span data-ttu-id="10ac2-111">tooconfigure intégration d’Azure AD avec Evidence.com, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="10ac2-111">tooconfigure Azure AD integration with Evidence.com, you need hello following items:</span></span>

- <span data-ttu-id="10ac2-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="10ac2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="10ac2-113">Un abonnement Evidence.com pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="10ac2-113">A Evidence.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="10ac2-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="10ac2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="10ac2-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="10ac2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="10ac2-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="10ac2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="10ac2-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="10ac2-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="10ac2-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="10ac2-118">Scenario description</span></span>
<span data-ttu-id="10ac2-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="10ac2-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="10ac2-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="10ac2-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="10ac2-121">Ajout de Evidence.com à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="10ac2-121">Adding Evidence.com from hello gallery</span></span>
2. <span data-ttu-id="10ac2-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="10ac2-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-evidencecom-from-hello-gallery"></a><span data-ttu-id="10ac2-123">Ajout de Evidence.com à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="10ac2-123">Adding Evidence.com from hello gallery</span></span>
<span data-ttu-id="10ac2-124">intégration de hello tooconfigure de Evidence.com dans Azure AD, vous devez tooadd Evidence.com à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="10ac2-124">tooconfigure hello integration of Evidence.com into Azure AD, you need tooadd Evidence.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="10ac2-125">**tooadd Evidence.com à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="10ac2-125">**tooadd Evidence.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="10ac2-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="10ac2-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="10ac2-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="10ac2-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="10ac2-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="10ac2-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="10ac2-133">Dans la zone de recherche de hello, tapez **Evidence.com**, sélectionnez **Evidence.com** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="10ac2-133">In hello search box, type **Evidence.com**, select **Evidence.com** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Evidence.com dans la liste des résultats hello](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="10ac2-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="10ac2-135">Configure and test Azure AD single sign-on</span></span>

<span data-ttu-id="10ac2-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Evidence.com avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="10ac2-136">In this section, you configure and test Azure AD single sign-on with Evidence.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="10ac2-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Evidence.com est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10ac2-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Evidence.com is tooa user in Azure AD.</span></span> <span data-ttu-id="10ac2-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Evidence.com doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="10ac2-138">In other words, a link relationship between an Azure AD user and hello related user in Evidence.com needs toobe established.</span></span>

<span data-ttu-id="10ac2-139">Dans Evidence.com, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="10ac2-139">In Evidence.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="10ac2-140">tooconfigure et test Azure AD l’authentification unique avec Evidence.com, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="10ac2-140">tooconfigure and test Azure AD single sign-on with Evidence.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="10ac2-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="10ac2-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="10ac2-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="10ac2-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="10ac2-143">**[Créer un utilisateur de test Evidence.com](#create-a-evidencecom-test-user)**  -toohave un équivalent de Britta Simon dans Evidence.com est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="10ac2-143">**[Create a Evidence.com test user](#create-a-evidencecom-test-user)** - toohave a counterpart of Britta Simon in Evidence.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="10ac2-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="10ac2-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="10ac2-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="10ac2-145">**[Test single sign-on](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="10ac2-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="10ac2-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="10ac2-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="10ac2-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Evidence.com application.</span></span>

<span data-ttu-id="10ac2-148">**tooconfigure Azure AD single sign-on avec Evidence.com, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="10ac2-148">**tooconfigure Azure AD single sign-on with Evidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="10ac2-149">Bonjour portail Azure, sur hello **Evidence.com** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-149">In hello Azure portal, on hello **Evidence.com** application integration page, click **Single sign-on**.</span></span>

    ![Lien Configurer l’authentification unique][4]

2. <span data-ttu-id="10ac2-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="10ac2-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_samlbase.png)

3. <span data-ttu-id="10ac2-153">Sur hello **Evidence.com domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="10ac2-153">On hello **Evidence.com Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_url.png)

    <span data-ttu-id="10ac2-155">a.</span><span class="sxs-lookup"><span data-stu-id="10ac2-155">a.</span></span> <span data-ttu-id="10ac2-156">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="10ac2-156">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    <span data-ttu-id="10ac2-157">b.</span><span class="sxs-lookup"><span data-stu-id="10ac2-157">b.</span></span> <span data-ttu-id="10ac2-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<yourtenant>.evidence.com`</span><span class="sxs-lookup"><span data-stu-id="10ac2-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<yourtenant>.evidence.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="10ac2-159">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="10ac2-159">These values are not real.</span></span> <span data-ttu-id="10ac2-160">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="10ac2-160">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="10ac2-161">Contact [équipe de support Client de Evidence.com](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="10ac2-161">Contact [Evidence.com Client support team](https://communities.taser.com/support/SupportContactUs?typ=LE) tooget these values.</span></span> 

4. <span data-ttu-id="10ac2-162">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="10ac2-162">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_certificate.png) 

5. <span data-ttu-id="10ac2-164">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="10ac2-164">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-evidence-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="10ac2-166">Sur hello **Evidence.com Configuration** , cliquez sur **Evidence.com de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="10ac2-166">On hello **Evidence.com Configuration** section, click **Configure Evidence.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="10ac2-167">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="10ac2-167">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configuration d’Evidence.com](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_configure.png) 

7. <span data-ttu-id="10ac2-169">Dans une fenêtre de navigateur web distinct, connexion tooyour Evidence.com locataire en tant qu’administrateur et accédez trop**Admin** onglet</span><span class="sxs-lookup"><span data-stu-id="10ac2-169">In a separate web browser window, login tooyour Evidence.com tenant as an administrator and navigate too**Admin** Tab</span></span>

8. <span data-ttu-id="10ac2-170">Cliquez sur **Agency Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="10ac2-170">Click on **Agency Single Sign On**</span></span>

9. <span data-ttu-id="10ac2-171">Sélectionnez **SAML Based Single Sign On**</span><span class="sxs-lookup"><span data-stu-id="10ac2-171">Select **SAML Based Single Sign On**</span></span>

10. <span data-ttu-id="10ac2-172">Hello de copie **ID d’entité SAML**, **SAML Sign-On URL du Service unique** et **URL de déconnexion** valeurs présentées dans hello portail Azure et les champs correspondants toohello Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="10ac2-172">Copy hello **SAML Entity ID**, **SAML Single Sign-On Service URL** and **Sign-Out URL** values shown in hello Azure portal and toohello corresponding fields in Evidence.com.</span></span>

11. <span data-ttu-id="10ac2-173">Ouvrez votre fichier Certificate(Base64) téléchargé dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat de sécurité** boîte.</span><span class="sxs-lookup"><span data-stu-id="10ac2-173">Open your downloaded Certificate(Base64) file in notepad, copy hello content of it into your clipboard, and then paste it toohello **Security Certificate** box.</span></span> 

12. <span data-ttu-id="10ac2-174">Enregistrer la configuration de hello dans Evidence.com.</span><span class="sxs-lookup"><span data-stu-id="10ac2-174">Save hello configuration in Evidence.com.</span></span>

> [!TIP]
> <span data-ttu-id="10ac2-175">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="10ac2-175">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="10ac2-176">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="10ac2-176">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="10ac2-177">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="10ac2-177">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="10ac2-178">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="10ac2-178">Create an Azure AD test user</span></span>

<span data-ttu-id="10ac2-179">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="10ac2-179">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

   ![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="10ac2-181">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="10ac2-181">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="10ac2-182">Bonjour portail Azure, dans le volet gauche de hello, cliquez sur hello **Azure Active Directory** bouton.</span><span class="sxs-lookup"><span data-stu-id="10ac2-182">In hello Azure portal, in hello left pane, click hello **Azure Active Directory** button.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-evidence-tutorial/create_aaduser_01.png)

2. <span data-ttu-id="10ac2-184">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes**, puis cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-184">toodisplay hello list of users, go too**Users and groups**, and then click **All users**.</span></span>

    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-evidence-tutorial/create_aaduser_02.png)

3. <span data-ttu-id="10ac2-186">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello hello **tous les utilisateurs** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="10ac2-186">tooopen hello **User** dialog box, click **Add** at hello top of hello **All Users** dialog box.</span></span>

    ![bouton Ajouter de Hello](./media/active-directory-saas-evidence-tutorial/create_aaduser_03.png)

4. <span data-ttu-id="10ac2-188">Bonjour **utilisateur** boîte de dialogue, exécutez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="10ac2-188">In hello **User** dialog box, perform hello following steps:</span></span>

    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-evidence-tutorial/create_aaduser_04.png)

    <span data-ttu-id="10ac2-190">a.</span><span class="sxs-lookup"><span data-stu-id="10ac2-190">a.</span></span> <span data-ttu-id="10ac2-191">Bonjour **nom** , tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-191">In hello **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="10ac2-192">b.</span><span class="sxs-lookup"><span data-stu-id="10ac2-192">b.</span></span> <span data-ttu-id="10ac2-193">Bonjour **nom d’utilisateur** zone, tapez Bonjour adresse de messagerie de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="10ac2-193">In hello **User name** box, type hello email address of user Britta Simon.</span></span>

    <span data-ttu-id="10ac2-194">c.</span><span class="sxs-lookup"><span data-stu-id="10ac2-194">c.</span></span> <span data-ttu-id="10ac2-195">Sélectionnez hello **afficher le mot de passe** case à cocher, puis écrire la valeur hello qui s’affiche dans hello **mot de passe** boîte.</span><span class="sxs-lookup"><span data-stu-id="10ac2-195">Select hello **Show Password** check box, and then write down hello value that's displayed in hello **Password** box.</span></span>

    <span data-ttu-id="10ac2-196">d.</span><span class="sxs-lookup"><span data-stu-id="10ac2-196">d.</span></span> <span data-ttu-id="10ac2-197">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-197">Click **Create**.</span></span>
 
### <a name="create-a-evidencecom-test-user"></a><span data-ttu-id="10ac2-198">Créer un utilisateur de test Evidence.com</span><span class="sxs-lookup"><span data-stu-id="10ac2-198">Create a Evidence.com test user</span></span>

<span data-ttu-id="10ac2-199">Pour Azure AD les utilisateurs toobe en mesure de toosign dans, ils doivent être configurés pour l’accès à l’intérieur de hello Evidence.com application.</span><span class="sxs-lookup"><span data-stu-id="10ac2-199">For Azure AD users toobe able toosign in, they must be provisioned for access inside hello Evidence.com application.</span></span> <span data-ttu-id="10ac2-200">Cette section décrit comment des comptes d’utilisateurs de toocreate Azure AD à l’intérieur de Evidence.com</span><span class="sxs-lookup"><span data-stu-id="10ac2-200">This section describes how toocreate Azure AD user accounts inside Evidence.com</span></span>

<span data-ttu-id="10ac2-201">**tooprovision un compte d’utilisateur dans Evidence.com :**</span><span class="sxs-lookup"><span data-stu-id="10ac2-201">**tooprovision a user account in Evidence.com:**</span></span>

1. <span data-ttu-id="10ac2-202">Dans une fenêtre de navigateur web, connectez-vous à votre site d’entreprise Evidence.com en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="10ac2-202">In a web browser window, log into your Evidence.com company site as an administrator.</span></span>

2. <span data-ttu-id="10ac2-203">Accédez trop**Admin** onglet.</span><span class="sxs-lookup"><span data-stu-id="10ac2-203">Navigate too**Admin** tab.</span></span>

3. <span data-ttu-id="10ac2-204">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-204">Click on **Add User**.</span></span>

4. <span data-ttu-id="10ac2-205">Cliquez sur hello **ajouter** bouton.</span><span class="sxs-lookup"><span data-stu-id="10ac2-205">Click hello **Add** button.</span></span>

5. <span data-ttu-id="10ac2-206">Hello **adresse de messagerie** Hello ajouté l’utilisateur doit correspondre au nom d’utilisateur hello d’utilisateurs de hello dans Azure AD souhaitant toogive accès.</span><span class="sxs-lookup"><span data-stu-id="10ac2-206">hello **Email Address** of hello added user must match hello username of hello users in Azure AD who you wish toogive access.</span></span> <span data-ttu-id="10ac2-207">Si hello nom d’utilisateur et votre adresse e-mail ne sont pas hello même valeur dans votre organisation, vous pouvez utiliser hello **Evidence.com > attributs > Single Sign-On** section de hello toochange portail Azure hello nameidenitifer envoyée adresse de messagerie tooEvidence.com toobe hello.</span><span class="sxs-lookup"><span data-stu-id="10ac2-207">If hello username and email address are not hello same value in your organization, you can use hello **Evidence.com > Attributes > Single Sign-On** section of hello Azure portal toochange hello nameidenitifer sent tooEvidence.com toobe hello email address.</span></span>

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="10ac2-208">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="10ac2-208">Assign hello Azure AD test user</span></span>

<span data-ttu-id="10ac2-209">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooEvidence.com.</span><span class="sxs-lookup"><span data-stu-id="10ac2-209">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEvidence.com.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="10ac2-211">**tooassign Britta Simon tooEvidence.com, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="10ac2-211">**tooassign Britta Simon tooEvidence.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="10ac2-212">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-212">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="10ac2-214">Dans la liste des applications hello, sélectionnez **Evidence.com**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-214">In hello applications list, select **Evidence.com**.</span></span>

    ![lien de Evidence.com Hello dans la liste des Applications hello](./media/active-directory-saas-evidence-tutorial/tutorial_evidence.com_app.png)  

3. <span data-ttu-id="10ac2-216">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-216">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202]

4. <span data-ttu-id="10ac2-218">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-218">Click **Add** button.</span></span> <span data-ttu-id="10ac2-219">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-219">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="10ac2-221">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="10ac2-221">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="10ac2-222">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-222">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="10ac2-223">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="10ac2-223">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="10ac2-224">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="10ac2-224">Test single sign-on</span></span>

<span data-ttu-id="10ac2-225">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="10ac2-225">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="10ac2-226">Lorsque vous cliquez sur mosaïque Evidence.com hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Evidence.com application.</span><span class="sxs-lookup"><span data-stu-id="10ac2-226">When you click hello Evidence.com tile in hello Access Panel, you should get automatically signed-on tooyour Evidence.com application.</span></span>
<span data-ttu-id="10ac2-227">Pour plus d’informations sur le volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="10ac2-227">For more information about the Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="10ac2-228">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="10ac2-228">Additional resources</span></span>

* [<span data-ttu-id="10ac2-229">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="10ac2-229">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="10ac2-230">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="10ac2-230">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-evidence-tutorial/tutorial_general_203.png

