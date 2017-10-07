---
title: "Didacticiel : intégration d’Azure Active Directory à Thoughtworks Mingle | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’occurrence."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 69d859d9-b7f7-4c42-bc8c-8036138be586
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jeedes
ms.openlocfilehash: c17f8e13d2db3de7d228d9b27128d134f98d6cdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-thoughtworks-mingle"></a><span data-ttu-id="b56de-103">Didacticiel : Intégration d’Azure AD à Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="b56de-103">Tutorial: Azure Active Directory integration with Thoughtworks Mingle</span></span>

<span data-ttu-id="b56de-104">Dans ce didacticiel, vous apprendrez comment toointegrate l’occurrence avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="b56de-104">In this tutorial, you learn how toointegrate Thoughtworks Mingle with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="b56de-105">Intégration de l’occurrence avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="b56de-105">Integrating Thoughtworks Mingle with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="b56de-106">Vous pouvez contrôler dans Azure AD qui a accès tooThoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="b56de-106">You can control in Azure AD who has access tooThoughtworks Mingle</span></span>
- <span data-ttu-id="b56de-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooThoughtworks Mingle (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="b56de-107">You can enable your users tooautomatically get signed-on tooThoughtworks Mingle (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="b56de-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="b56de-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="b56de-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="b56de-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b56de-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b56de-110">Prerequisites</span></span>

<span data-ttu-id="b56de-111">tooconfigure intégration d’Azure AD avec l’occurrence, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="b56de-111">tooconfigure Azure AD integration with Thoughtworks Mingle, you need hello following items:</span></span>

- <span data-ttu-id="b56de-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="b56de-112">An Azure AD subscription</span></span>
- <span data-ttu-id="b56de-113">Un abonnement Thoughtworks Mingle pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="b56de-113">A Thoughtworks Mingle single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="b56de-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b56de-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="b56de-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="b56de-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="b56de-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b56de-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="b56de-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="b56de-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="b56de-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="b56de-118">Scenario description</span></span>
<span data-ttu-id="b56de-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="b56de-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="b56de-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="b56de-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="b56de-121">Ajout de l’occurrence de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b56de-121">Adding Thoughtworks Mingle from hello gallery</span></span>
2. <span data-ttu-id="b56de-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b56de-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-thoughtworks-mingle-from-hello-gallery"></a><span data-ttu-id="b56de-123">Ajout de l’occurrence de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="b56de-123">Adding Thoughtworks Mingle from hello gallery</span></span>
<span data-ttu-id="b56de-124">tooconfigure hello intégration de l’occurrence dans Azure AD, vous devez tooadd Thoughtworks Mingle à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="b56de-124">tooconfigure hello integration of Thoughtworks Mingle into Azure AD, you need tooadd Thoughtworks Mingle from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="b56de-125">**tooadd Thoughtworks Mingle à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b56de-125">**tooadd Thoughtworks Mingle from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="b56de-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="b56de-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![bouton d’Azure Active Directory Hello][1]

2. <span data-ttu-id="b56de-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="b56de-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="b56de-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b56de-129">Then go too**All applications**.</span></span>

    ![panneau des applications Enterprise Hello][2]
    
3. <span data-ttu-id="b56de-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="b56de-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Nouveau bouton d’application Hello][3]

4. <span data-ttu-id="b56de-133">Dans la zone de recherche de hello, tapez **Thoughtworks Mingle**, sélectionnez **Thoughtworks Mingle** à partir du volet de résultats, puis sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="b56de-133">In hello search box, type **Thoughtworks Mingle**, select **Thoughtworks Mingle** from result panel then click **Add** button tooadd hello application.</span></span>

    ![Liste des résultats de l’occurrence Bonjour](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="b56de-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b56de-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="b56de-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Thoughtworks Mingle avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="b56de-136">In this section, you configure and test Azure AD single sign-on with Thoughtworks Mingle based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="b56de-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent de hello en l’occurrence est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b56de-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Thoughtworks Mingle is tooa user in Azure AD.</span></span> <span data-ttu-id="b56de-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello en l’occurrence doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="b56de-138">In other words, a link relationship between an Azure AD user and hello related user in Thoughtworks Mingle needs toobe established.</span></span>

<span data-ttu-id="b56de-139">En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="b56de-139">In Thoughtworks Mingle, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="b56de-140">tooconfigure et test Azure AD l’authentification unique avec l’occurrence, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="b56de-140">tooconfigure and test Azure AD single sign-on with Thoughtworks Mingle, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="b56de-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="b56de-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="b56de-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="b56de-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="b56de-143">**[Créer un utilisateur test Thoughtworks Mingle](#create-a-thoughtworks-mingle-test-user)**  -toohave un équivalent de Britta Simon en l’occurrence qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b56de-143">**[Create a Thoughtworks Mingle test user](#create-a-thoughtworks-mingle-test-user)** - toohave a counterpart of Britta Simon in Thoughtworks Mingle that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="b56de-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b56de-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="b56de-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="b56de-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="b56de-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="b56de-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="b56de-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application l’occurrence.</span><span class="sxs-lookup"><span data-stu-id="b56de-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Thoughtworks Mingle application.</span></span>

<span data-ttu-id="b56de-148">**tooconfigure Azure AD single sign-on avec l’occurrence, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b56de-148">**tooconfigure Azure AD single sign-on with Thoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="b56de-149">Bonjour portail Azure, sur hello **Thoughtworks Mingle** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="b56de-149">In hello Azure portal, on hello **Thoughtworks Mingle** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="b56de-151">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="b56de-151">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_samlbase.png)

3. <span data-ttu-id="b56de-153">Sur hello **URL et le domaine de Thoughtworks Mingle** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b56de-153">On hello **Thoughtworks Mingle Domain and URLs** section, perform hello following steps:</span></span>

    ![Informations d’authentification unique dans Domaine et URL Thoughtworks Mingle](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_url.png)

    <span data-ttu-id="b56de-155">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.mingle.thoughtworks.com`</span><span class="sxs-lookup"><span data-stu-id="b56de-155">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.mingle.thoughtworks.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b56de-156">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="b56de-156">hello value is not real.</span></span> <span data-ttu-id="b56de-157">Valeur de hello de mise à jour avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="b56de-157">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="b56de-158">Contact [équipe de support Client de Thoughtworks Mingle](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="b56de-158">Contact [Thoughtworks Mingle Client support team](https://support.thoughtworks.com/hc/categories/201743486-Mingle-Community-Support) tooget hello value.</span></span> 
 
4. <span data-ttu-id="b56de-159">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="b56de-159">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![lien de téléchargement du certificat Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_certificate.png) 

5. <span data-ttu-id="b56de-161">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="b56de-161">Click **Save** button.</span></span>

    ![Bouton Enregistrer de la page Configurer l’authentification unique](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="b56de-163">Connectez-vous à tooyour **Thoughtworks Mingle** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b56de-163">Log in tooyour **Thoughtworks Mingle** company site as administrator.</span></span>

7. <span data-ttu-id="b56de-164">Cliquez sur hello **Admin** onglet et cliquez ensuite sur **SSO Config**.</span><span class="sxs-lookup"><span data-stu-id="b56de-164">Click hello **Admin** tab, and then, click **SSO Config**.</span></span>
   
    <span data-ttu-id="b56de-165">![Onglet Admin](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "Configuration SSO")</span><span class="sxs-lookup"><span data-stu-id="b56de-165">![Admin tab](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785157.png "SSO Config")</span></span>

8. <span data-ttu-id="b56de-166">Bonjour **SSO Config** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b56de-166">In hello **SSO Config** section, perform hello following steps:</span></span>
   
    <span data-ttu-id="b56de-167">![Configuration de l’authentification unique](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "Configuration de l’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="b56de-167">![SSO Config](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785158.png "SSO Config")</span></span>
    
    <span data-ttu-id="b56de-168">a.</span><span class="sxs-lookup"><span data-stu-id="b56de-168">a.</span></span> <span data-ttu-id="b56de-169">fichier de métadonnées tooupload hello, cliquez sur **choisir un fichier**.</span><span class="sxs-lookup"><span data-stu-id="b56de-169">tooupload hello metadata file, click **Choose file**.</span></span> 

    <span data-ttu-id="b56de-170">b.</span><span class="sxs-lookup"><span data-stu-id="b56de-170">b.</span></span> <span data-ttu-id="b56de-171">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="b56de-171">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="b56de-172">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="b56de-172">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="b56de-173">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="b56de-173">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="b56de-174">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="b56de-174">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="b56de-175">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="b56de-175">Create an Azure AD test user</span></span>
<span data-ttu-id="b56de-176">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="b56de-176">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur de test Azure AD][100]

<span data-ttu-id="b56de-178">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b56de-178">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="b56de-179">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="b56de-179">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![bouton d’Azure Active Directory Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="b56de-181">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b56de-181">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Hello « Utilisateurs et groupes » et « Tous les utilisateurs » liens](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="b56de-183">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="b56de-183">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![bouton Ajouter de Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="b56de-185">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b56de-185">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![boîte de dialogue utilisateur Hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="b56de-187">a.</span><span class="sxs-lookup"><span data-stu-id="b56de-187">a.</span></span> <span data-ttu-id="b56de-188">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="b56de-188">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="b56de-189">b.</span><span class="sxs-lookup"><span data-stu-id="b56de-189">b.</span></span> <span data-ttu-id="b56de-190">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="b56de-190">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="b56de-191">c.</span><span class="sxs-lookup"><span data-stu-id="b56de-191">c.</span></span> <span data-ttu-id="b56de-192">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="b56de-192">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="b56de-193">d.</span><span class="sxs-lookup"><span data-stu-id="b56de-193">d.</span></span> <span data-ttu-id="b56de-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="b56de-194">Click **Create**.</span></span>
 
### <a name="create-a-thoughtworks-mingle-test-user"></a><span data-ttu-id="b56de-195">Créer un utilisateur de test Thoughtworks Mingle</span><span class="sxs-lookup"><span data-stu-id="b56de-195">Create a Thoughtworks Mingle test user</span></span>

<span data-ttu-id="b56de-196">Pour Azure AD les utilisateurs toobe en mesure de toosign dans, ils doivent être mis en service toohello application Thoughtworks Mingle à l’aide de leur nom d’utilisateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b56de-196">For Azure AD users toobe able toosign in, they must be provisioned toohello Thoughtworks Mingle application using their Azure Active Directory user names.</span></span> <span data-ttu-id="b56de-197">Dans les cas de hello de l’occurrence, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="b56de-197">In hello case of Thoughtworks Mingle, provisioning is a manual task.</span></span>

<span data-ttu-id="b56de-198">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b56de-198">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="b56de-199">Ouvrez une session dans tooyour site d’entreprise Thoughtworks Mingle en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="b56de-199">Log in tooyour Thoughtworks Mingle company site as administrator.</span></span>

2. <span data-ttu-id="b56de-200">Cliquez sur **Profile**.</span><span class="sxs-lookup"><span data-stu-id="b56de-200">Click **Profile**.</span></span>
   
    <span data-ttu-id="b56de-201">![Votre premier projet](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Votre premier projet")</span><span class="sxs-lookup"><span data-stu-id="b56de-201">![Your First Project](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785160.png "Your First Project")</span></span>

3. <span data-ttu-id="b56de-202">Cliquez sur hello **Admin** onglet, puis cliquez sur **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="b56de-202">Click hello **Admin** tab, and then click **Users**.</span></span>
   
    <span data-ttu-id="b56de-203">![Utilisateurs](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="b56de-203">![Users](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785161.png "Users")</span></span>

4. <span data-ttu-id="b56de-204">Cliquez sur **New User**.</span><span class="sxs-lookup"><span data-stu-id="b56de-204">Click **New User**.</span></span>
   
    <span data-ttu-id="b56de-205">![Nouvel utilisateur](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="b56de-205">![New User](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785162.png "New User")</span></span>

5. <span data-ttu-id="b56de-206">Sur hello **nouvel utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="b56de-206">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    <span data-ttu-id="b56de-207">![Boîte de dialogue Nouvel utilisateur](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "Nouvel utilisateur")</span><span class="sxs-lookup"><span data-stu-id="b56de-207">![New User dialog](./media/active-directory-saas-thoughtworks-mingle-tutorial/ic785163.png "New User")</span></span>  
 
    <span data-ttu-id="b56de-208">a.</span><span class="sxs-lookup"><span data-stu-id="b56de-208">a.</span></span> <span data-ttu-id="b56de-209">Hello de type **nom de connexion**, **nom d’affichage**, **choisir un mot de passe**, **confirmer le mot de passe** d’un Azure valide compte AD tooprovision dans hello liés les zones de texte.</span><span class="sxs-lookup"><span data-stu-id="b56de-209">Type hello **Sign-in name**, **Display name**, **Choose password**, **Confirm password** of a valid Azure AD account you want tooprovision into hello related textboxes.</span></span> 

    <span data-ttu-id="b56de-210">b.</span><span class="sxs-lookup"><span data-stu-id="b56de-210">b.</span></span> <span data-ttu-id="b56de-211">Dans **User type (Type d’utilisateur)**, sélectionnez **Full user (Utilisateur complet)**.</span><span class="sxs-lookup"><span data-stu-id="b56de-211">As **User type**, select **Full user**.</span></span>

    <span data-ttu-id="b56de-212">c.</span><span class="sxs-lookup"><span data-stu-id="b56de-212">c.</span></span> <span data-ttu-id="b56de-213">Cliquez sur **Create This Profile**.</span><span class="sxs-lookup"><span data-stu-id="b56de-213">Click **Create This Profile**.</span></span>

>[!NOTE]
><span data-ttu-id="b56de-214">Vous pouvez utiliser n’importe quel autre Thoughtworks Mingle utilisateur compte outil de création ou API fournie par Thoughtworks Mingle de tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="b56de-214">You can use any other Thoughtworks Mingle user account creation tools or APIs provided by Thoughtworks Mingle tooprovision AAD user accounts.</span></span>
> 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="b56de-215">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="b56de-215">Assign hello Azure AD test user</span></span>

<span data-ttu-id="b56de-216">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooThoughtworks Mingle.</span><span class="sxs-lookup"><span data-stu-id="b56de-216">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooThoughtworks Mingle.</span></span>

![Attribuer le rôle d’utilisateur hello][200] 

<span data-ttu-id="b56de-218">**tooassign Britta Simon tooThoughtworks Mingle, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="b56de-218">**tooassign Britta Simon tooThoughtworks Mingle, perform hello following steps:**</span></span>

1. <span data-ttu-id="b56de-219">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="b56de-219">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="b56de-221">Dans la liste des applications hello, sélectionnez **Thoughtworks Mingle**.</span><span class="sxs-lookup"><span data-stu-id="b56de-221">In hello applications list, select **Thoughtworks Mingle**.</span></span>

    ![lien de l’occurrence Hello dans la liste des Applications hello](./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_thoughtworksmingle_app.png) 

3. <span data-ttu-id="b56de-223">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b56de-223">In hello menu on hello left, click **Users and groups**.</span></span>

    ![lien de « Utilisateurs et groupes » Hello][202] 

4. <span data-ttu-id="b56de-225">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b56de-225">Click **Add** button.</span></span> <span data-ttu-id="b56de-226">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b56de-226">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![volet d’ajouter l’affectation de Hello][203]

5. <span data-ttu-id="b56de-228">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="b56de-228">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="b56de-229">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="b56de-229">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="b56de-230">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="b56de-230">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="b56de-231">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="b56de-231">Test single sign-on</span></span>

<span data-ttu-id="b56de-232">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="b56de-232">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="b56de-233">Lorsque vous cliquez sur mosaïque de l’occurrence hello Bonjour volet d’accès, vous devez obtenir l’application de l’occurrence tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="b56de-233">When you click hello Thoughtworks Mingle tile in hello Access Panel, you should get automatically signed-on tooyour Thoughtworks Mingle application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="b56de-234">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="b56de-234">Additional resources</span></span>

* [<span data-ttu-id="b56de-235">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b56de-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="b56de-236">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="b56de-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-thoughtworks-mingle-tutorial/tutorial_general_203.png

