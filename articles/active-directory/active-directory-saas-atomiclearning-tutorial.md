---
title: "Didacticiel : Intégration d’Azure Active Directory avec Atomic Learning | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’apprentissage atomique."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 495f54a6-e6c4-41b0-aafa-a6283d33efc8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: jeedes
ms.openlocfilehash: 12d7c380dbe47899eb35486c5e2a6936e8fb8b3a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-atomic-learning"></a><span data-ttu-id="a68ac-103">Didacticiel : Intégration d’Azure Active Directory à Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="a68ac-103">Tutorial: Azure Active Directory integration with Atomic Learning</span></span>

<span data-ttu-id="a68ac-104">Dans ce didacticiel, vous apprendrez comment toointegrate Learning atomique avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a68ac-104">In this tutorial, you learn how toointegrate Atomic Learning with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="a68ac-105">Intégration de formation atomique avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a68ac-105">Integrating Atomic Learning with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="a68ac-106">Vous pouvez contrôler dans Azure AD qui a accès tooAtomic d’apprentissage</span><span class="sxs-lookup"><span data-stu-id="a68ac-106">You can control in Azure AD who has access tooAtomic Learning</span></span>
- <span data-ttu-id="a68ac-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAtomic Learning (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="a68ac-107">You can enable your users tooautomatically get signed-on tooAtomic Learning (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="a68ac-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="a68ac-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="a68ac-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="a68ac-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a68ac-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a68ac-110">Prerequisites</span></span>

<span data-ttu-id="a68ac-111">tooconfigure intégration d’Azure AD avec Learning atomique, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="a68ac-111">tooconfigure Azure AD integration with Atomic Learning, you need hello following items:</span></span>

- <span data-ttu-id="a68ac-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="a68ac-112">An Azure AD subscription</span></span>
- <span data-ttu-id="a68ac-113">Un abonnement Atomic Learning pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="a68ac-113">An Atomic Learning single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="a68ac-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="a68ac-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="a68ac-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="a68ac-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="a68ac-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a68ac-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="a68ac-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a68ac-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="a68ac-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="a68ac-118">Scenario description</span></span>
<span data-ttu-id="a68ac-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="a68ac-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="a68ac-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="a68ac-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="a68ac-121">Ajout d’apprentissage atomique à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a68ac-121">Adding Atomic Learning from hello gallery</span></span>
2. <span data-ttu-id="a68ac-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a68ac-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-atomic-learning-from-hello-gallery"></a><span data-ttu-id="a68ac-123">Ajout d’apprentissage atomique à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="a68ac-123">Adding Atomic Learning from hello gallery</span></span>
<span data-ttu-id="a68ac-124">tooconfigure hello intégration de la formation atomique dans Azure AD, vous devez tooadd atomique Learning à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="a68ac-124">tooconfigure hello integration of Atomic Learning into Azure AD, you need tooadd Atomic Learning from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="a68ac-125">**tooadd atomique d’apprentissage à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a68ac-125">**tooadd Atomic Learning from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="a68ac-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a68ac-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="a68ac-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="a68ac-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="a68ac-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a68ac-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="a68ac-133">Dans la zone de recherche de hello, tapez **atomique Learning**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-133">In hello search box, type **Atomic Learning**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_search.png)

5. <span data-ttu-id="a68ac-135">Dans le volet de résultats hello, sélectionnez **Learning atomique**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="a68ac-135">In hello results panel, select **Atomic Learning**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="a68ac-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a68ac-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="a68ac-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec Atomic Learning au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="a68ac-138">In this section, you configure and test Azure AD single sign-on with Atomic Learning based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="a68ac-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Learning atomique est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a68ac-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Atomic Learning is tooa user in Azure AD.</span></span> <span data-ttu-id="a68ac-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello atomique pour la formation doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="a68ac-140">In other words, a link relationship between an Azure AD user and hello related user in Atomic Learning needs toobe established.</span></span>

<span data-ttu-id="a68ac-141">En savoir atomique, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="a68ac-141">In Atomic Learning, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="a68ac-142">tooconfigure et test Azure AD l’authentification unique avec Learning atomique, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="a68ac-142">tooconfigure and test Azure AD single sign-on with Atomic Learning, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="a68ac-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a68ac-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="a68ac-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="a68ac-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="a68ac-145">**[Création d’un utilisateur de test de formation atomique](#creating-an-atomic-learning-test-user)**  -toohave un équivalent de Britta Simon dans Learning atomique qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a68ac-145">**[Creating an Atomic Learning test user](#creating-an-atomic-learning-test-user)** - toohave a counterpart of Britta Simon in Atomic Learning that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="a68ac-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a68ac-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="a68ac-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="a68ac-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="a68ac-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="a68ac-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="a68ac-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de formation atomique.</span><span class="sxs-lookup"><span data-stu-id="a68ac-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Atomic Learning application.</span></span>

<span data-ttu-id="a68ac-150">**tooconfigure Azure AD single sign-on avec atomique d’apprentissage, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a68ac-150">**tooconfigure Azure AD single sign-on with Atomic Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="a68ac-151">Bonjour portail Azure, sur hello **Learning atomique** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-151">In hello Azure portal, on hello **Atomic Learning** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="a68ac-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="a68ac-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_samlbase.png)

3. <span data-ttu-id="a68ac-155">Sur hello **atomique Learning domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a68ac-155">On hello **Atomic Learning Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_url.png)

     <span data-ttu-id="a68ac-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="a68ac-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://secure2.atomiclearning.com/sso/shibboleth/<companyname>`</span></span>
    
    > [!NOTE] 
    > <span data-ttu-id="a68ac-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="a68ac-158">This value is not real.</span></span> <span data-ttu-id="a68ac-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="a68ac-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="a68ac-160">Contact [équipe de support Client de formation atomique](mailto:cs@atomiclearning.com) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="a68ac-160">Contact [Atomic Learning Client support team](mailto:cs@atomiclearning.com) tooget this value.</span></span> 
 
4. <span data-ttu-id="a68ac-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="a68ac-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_certificate.png) 

5. <span data-ttu-id="a68ac-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="a68ac-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="a68ac-165">tooconfigure l’authentification unique sur **Learning atomique** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support technique d’apprentissage atomique](mailto:cs@atomiclearning.com).</span><span class="sxs-lookup"><span data-stu-id="a68ac-165">tooconfigure single sign-on on **Atomic Learning** side, you need toosend hello downloaded **Metadata XML** too[Atomic Learning support team](mailto:cs@atomiclearning.com).</span></span> <span data-ttu-id="a68ac-166">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="a68ac-166">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="a68ac-167">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="a68ac-167">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="a68ac-168">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="a68ac-168">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="a68ac-169">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="a68ac-169">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="a68ac-170">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="a68ac-170">Creating an Azure AD test user</span></span>
<span data-ttu-id="a68ac-171">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="a68ac-171">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="a68ac-173">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a68ac-173">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="a68ac-174">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="a68ac-174">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="a68ac-176">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-176">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="a68ac-178">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="a68ac-178">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="a68ac-180">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="a68ac-180">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-atomiclearning-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="a68ac-182">a.</span><span class="sxs-lookup"><span data-stu-id="a68ac-182">a.</span></span> <span data-ttu-id="a68ac-183">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-183">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="a68ac-184">b.</span><span class="sxs-lookup"><span data-stu-id="a68ac-184">b.</span></span> <span data-ttu-id="a68ac-185">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="a68ac-185">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="a68ac-186">c.</span><span class="sxs-lookup"><span data-stu-id="a68ac-186">c.</span></span> <span data-ttu-id="a68ac-187">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-187">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="a68ac-188">d.</span><span class="sxs-lookup"><span data-stu-id="a68ac-188">d.</span></span> <span data-ttu-id="a68ac-189">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-189">Click **Create**.</span></span>
 
### <a name="creating-an-atomic-learning-test-user"></a><span data-ttu-id="a68ac-190">Création d’un utilisateur de test Atomic Learning</span><span class="sxs-lookup"><span data-stu-id="a68ac-190">Creating an Atomic Learning test user</span></span>

<span data-ttu-id="a68ac-191">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Atomic Learning.</span><span class="sxs-lookup"><span data-stu-id="a68ac-191">In this section, you create a user called Britta Simon in Atomic Learning.</span></span> <span data-ttu-id="a68ac-192">Atomic Learning prend en charge l’approvisionnement juste-à-temps, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="a68ac-192">Atomic Learning supports just-in-time provisioning, which is by default enabled.</span></span> 

<span data-ttu-id="a68ac-193">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="a68ac-193">There is no action item for you in this section.</span></span> <span data-ttu-id="a68ac-194">Un nouvel utilisateur est créé pendant un tooaccess tentative Learning atomique s’il n’existe pas encore à l’aide d’adresse de messagerie hello pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="a68ac-194">A new user is created during an attempt tooaccess Atomic Learning if it doesn't exist yet using hello email address for hello user.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="a68ac-195">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="a68ac-195">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="a68ac-196">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAtomic d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="a68ac-196">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAtomic Learning.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="a68ac-198">**tooassign Britta Simon tooAtomic de formation, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="a68ac-198">**tooassign Britta Simon tooAtomic Learning, perform hello following steps:**</span></span>

1. <span data-ttu-id="a68ac-199">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-199">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="a68ac-201">Dans la liste des applications hello, sélectionnez **atomique Learning**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-201">In hello applications list, select **Atomic Learning**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-atomiclearning-tutorial/tutorial_atomiclearning_app.png) 

3. <span data-ttu-id="a68ac-203">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-203">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="a68ac-205">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-205">Click **Add** button.</span></span> <span data-ttu-id="a68ac-206">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-206">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="a68ac-208">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="a68ac-208">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="a68ac-209">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-209">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="a68ac-210">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="a68ac-210">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="a68ac-211">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="a68ac-211">Testing single sign-on</span></span>

<span data-ttu-id="a68ac-212">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="a68ac-212">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="a68ac-213">Lorsque vous cliquez sur mosaïque de formation atomique hello Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour application de formation atomique.</span><span class="sxs-lookup"><span data-stu-id="a68ac-213">When you click hello Atomic Learning tile in hello Access Panel, you should get automatically signed-on tooyour Atomic Learning application.</span></span>
<span data-ttu-id="a68ac-214">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a68ac-214">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="a68ac-215">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="a68ac-215">Additional resources</span></span>

* [<span data-ttu-id="a68ac-216">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a68ac-216">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="a68ac-217">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="a68ac-217">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-atomiclearning-tutorial/tutorial_general_203.png

