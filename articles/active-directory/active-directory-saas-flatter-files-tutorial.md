---
title: "Didacticiel : Intégration d’Azure AD à Flatter Files | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et les fichiers plate."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: f86fe5e3-0e91-40d6-869c-3df6912d27ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/21/2017
ms.author: jeedes
ms.openlocfilehash: 73ca2613b7bbaf9992ecf624ff5defabaa44f7a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-flatter-files"></a><span data-ttu-id="12820-103">Didacticiel : Intégration d’Azure Active Directory à Flatter Files</span><span class="sxs-lookup"><span data-stu-id="12820-103">Tutorial: Azure Active Directory integration with Flatter Files</span></span>

<span data-ttu-id="12820-104">Dans ce didacticiel, vous apprendrez comment toointegrate fichiers plate avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="12820-104">In this tutorial, you learn how toointegrate Flatter Files with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="12820-105">Intégration des fichiers plate avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="12820-105">Integrating Flatter Files with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="12820-106">Vous pouvez contrôler dans Azure AD qui a accès aux fichiers de tooFlatter</span><span class="sxs-lookup"><span data-stu-id="12820-106">You can control in Azure AD who has access tooFlatter Files</span></span>
- <span data-ttu-id="12820-107">Vous pouvez activer votre tooautomatically utilisateurs obtenir les fichiers signés sur tooFlatter (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="12820-107">You can enable your users tooautomatically get signed-on tooFlatter Files (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="12820-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="12820-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="12820-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="12820-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12820-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="12820-110">Prerequisites</span></span>

<span data-ttu-id="12820-111">tooconfigure intégration d’Azure AD avec des fichiers plate, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="12820-111">tooconfigure Azure AD integration with Flatter Files, you need hello following items:</span></span>

- <span data-ttu-id="12820-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="12820-112">An Azure AD subscription</span></span>
- <span data-ttu-id="12820-113">Un abonnement Flatter Files pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="12820-113">A Flatter Files single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="12820-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="12820-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="12820-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="12820-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="12820-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="12820-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="12820-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="12820-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="12820-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="12820-118">Scenario description</span></span>
<span data-ttu-id="12820-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="12820-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="12820-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="12820-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="12820-121">Ajout de fichiers plate à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="12820-121">Adding Flatter Files from hello gallery</span></span>
2. <span data-ttu-id="12820-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="12820-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-flatter-files-from-hello-gallery"></a><span data-ttu-id="12820-123">Ajout de fichiers plate à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="12820-123">Adding Flatter Files from hello gallery</span></span>
<span data-ttu-id="12820-124">tooconfigure hello intégration des fichiers plate dans Azure AD, vous devez tooadd plate des fichiers à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="12820-124">tooconfigure hello integration of Flatter Files into Azure AD, you need tooadd Flatter Files from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="12820-125">**tooadd plate des fichiers à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="12820-125">**tooadd Flatter Files from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="12820-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="12820-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="12820-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="12820-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="12820-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="12820-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="12820-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="12820-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="12820-133">Dans la zone de recherche de hello, tapez **fichiers plate**.</span><span class="sxs-lookup"><span data-stu-id="12820-133">In hello search box, type **Flatter Files**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_search.png)

5. <span data-ttu-id="12820-135">Dans le volet de résultats hello, sélectionnez **fichiers plate**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="12820-135">In hello results panel, select **Flatter Files**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="12820-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="12820-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="12820-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Flatter Files avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="12820-138">In this section, you configure and test Azure AD single sign-on with Flatter Files based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="12820-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans les fichiers plate est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12820-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Flatter Files is tooa user in Azure AD.</span></span> <span data-ttu-id="12820-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur dans les fichiers plate hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="12820-140">In other words, a link relationship between an Azure AD user and hello related user in Flatter Files needs toobe established.</span></span>

<span data-ttu-id="12820-141">Dans les fichiers plate, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="12820-141">In Flatter Files, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="12820-142">tooconfigure et test Azure AD l’authentification unique avec des fichiers plate, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="12820-142">tooconfigure and test Azure AD single sign-on with Flatter Files, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="12820-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="12820-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="12820-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="12820-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="12820-145">**[Création d’un utilisateur de test plus plate des fichiers](#creating-a-flatter-files-test-user)**  -toohave un équivalent de Britta Simon dans les fichiers plate qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="12820-145">**[Creating a Flatter Files test user](#creating-a-flatter-files-test-user)** - toohave a counterpart of Britta Simon in Flatter Files that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="12820-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="12820-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="12820-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="12820-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="12820-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="12820-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="12820-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application de fichiers plate.</span><span class="sxs-lookup"><span data-stu-id="12820-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Flatter Files application.</span></span>

<span data-ttu-id="12820-150">**tooconfigure Azure AD authentification unique avec des fichiers plate, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="12820-150">**tooconfigure Azure AD single sign-on with Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="12820-151">Bonjour portail Azure, sur hello **fichiers plate** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="12820-151">In hello Azure portal, on hello **Flatter Files** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="12820-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="12820-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_samlbase.png)

3. <span data-ttu-id="12820-155">Sur hello **plate domaine de fichiers et les URL** section, hello utilisateur n’est pas tooperform toutes les étapes que l’application hello est déjà pré-intégration à Azure.</span><span class="sxs-lookup"><span data-stu-id="12820-155">On hello **Flatter Files Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_url.png)
 
4. <span data-ttu-id="12820-157">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="12820-157">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_certificate.png) 

5. <span data-ttu-id="12820-159">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="12820-159">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="12820-161">Sur hello **plate fichiers Configuration** , cliquez sur **configurer les fichiers plate** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="12820-161">On hello **Flatter Files Configuration** section, click **Configure Flatter Files** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="12820-162">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="12820-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_configure.png) 

7. <span data-ttu-id="12820-164">Authentification tooyour application fichiers plate en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="12820-164">Sign-on tooyour Flatter Files application as an administrator.</span></span>

8. <span data-ttu-id="12820-165">Cliquez sur **TABLEAU DE BORD**.</span><span class="sxs-lookup"><span data-stu-id="12820-165">Click **DASHBOARD**.</span></span> 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_05.png)  

9. <span data-ttu-id="12820-167">Cliquez sur **paramètres**, puis exécutez hello comme suit sur hello **société** onglet :</span><span class="sxs-lookup"><span data-stu-id="12820-167">Click **Settings**, and then perform hello following steps on hello **Company** tab:</span></span> 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_06.png)  
    
    <span data-ttu-id="12820-169">a.</span><span class="sxs-lookup"><span data-stu-id="12820-169">a.</span></span> <span data-ttu-id="12820-170">Sélectionnez **Use SAML 2.0 for Authentication**.</span><span class="sxs-lookup"><span data-stu-id="12820-170">Select **Use SAML 2.0 for Authentication**.</span></span>
    
    <span data-ttu-id="12820-171">b.</span><span class="sxs-lookup"><span data-stu-id="12820-171">b.</span></span> <span data-ttu-id="12820-172">Cliquez sur **Configure SAML**.</span><span class="sxs-lookup"><span data-stu-id="12820-172">Click **Configure SAML**.</span></span>

8. <span data-ttu-id="12820-173">Sur hello **Configuration SAML** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="12820-173">On hello **SAML Configuration** dialog, perform hello following steps:</span></span> 
   
    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_08.png)  
   
    <span data-ttu-id="12820-175">a.</span><span class="sxs-lookup"><span data-stu-id="12820-175">a.</span></span> <span data-ttu-id="12820-176">Bonjour **domaine** zone de texte, tapez votre domaine inscrit.</span><span class="sxs-lookup"><span data-stu-id="12820-176">In hello **Domain** textbox, type your registered domain.</span></span>
   
    >[!NOTE]
    ><span data-ttu-id="12820-177">Si vous n’avez pas encore de domaine enregistré, contactez votre équipe de support Flatter Files via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span><span class="sxs-lookup"><span data-stu-id="12820-177">If you don't have a registered domain yet, contact your Flatter Files support team via [support@flatterfiles.com](mailto:support@flatterfiles.com).</span></span> 
    
    <span data-ttu-id="12820-178">b.</span><span class="sxs-lookup"><span data-stu-id="12820-178">b.</span></span> <span data-ttu-id="12820-179">Dans **URL du fournisseur d’identité** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié forment le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="12820-179">In **Identity Provider URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied form Azure portal.</span></span>
   
    <span data-ttu-id="12820-180">c.</span><span class="sxs-lookup"><span data-stu-id="12820-180">c.</span></span>  <span data-ttu-id="12820-181">Ouvrez votre certificat codé en base 64 dans le bloc-notes, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat de fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="12820-181">Open your base-64 encoded certificate in notepad, copy hello content of it into your clipboard, and then paste it toohello **Identity Provider Certificate** textbox.</span></span>

    <span data-ttu-id="12820-182">d.</span><span class="sxs-lookup"><span data-stu-id="12820-182">d.</span></span> <span data-ttu-id="12820-183">Cliquez sur **Update**.</span><span class="sxs-lookup"><span data-stu-id="12820-183">Click **Update**.</span></span>

> [!TIP]
> <span data-ttu-id="12820-184">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="12820-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="12820-185">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="12820-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="12820-186">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="12820-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="12820-187">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="12820-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="12820-188">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="12820-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="12820-190">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="12820-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="12820-191">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="12820-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="12820-193">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="12820-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="12820-195">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="12820-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="12820-197">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="12820-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-flatter-files-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="12820-199">a.</span><span class="sxs-lookup"><span data-stu-id="12820-199">a.</span></span> <span data-ttu-id="12820-200">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="12820-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="12820-201">b.</span><span class="sxs-lookup"><span data-stu-id="12820-201">b.</span></span> <span data-ttu-id="12820-202">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="12820-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="12820-203">c.</span><span class="sxs-lookup"><span data-stu-id="12820-203">c.</span></span> <span data-ttu-id="12820-204">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="12820-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="12820-205">d.</span><span class="sxs-lookup"><span data-stu-id="12820-205">d.</span></span> <span data-ttu-id="12820-206">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="12820-206">Click **Create**.</span></span>
 
### <a name="creating-a-flatter-files-test-user"></a><span data-ttu-id="12820-207">Création d’un utilisateur de test Flatter Files</span><span class="sxs-lookup"><span data-stu-id="12820-207">Creating a Flatter Files test user</span></span>

<span data-ttu-id="12820-208">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans les fichiers plate.</span><span class="sxs-lookup"><span data-stu-id="12820-208">hello objective of this section is toocreate a user called Britta Simon in Flatter Files.</span></span>

<span data-ttu-id="12820-209">**toocreate un utilisateur appelé Britta Simon dans les fichiers plate, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="12820-209">**toocreate a user called Britta Simon in Flatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="12820-210">Ouverture de session tooyour **fichiers plate** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="12820-210">Sign on tooyour **Flatter Files** company site as administrator.</span></span>

2. <span data-ttu-id="12820-211">Dans le volet de navigation hello hello gauche, cliquez sur **paramètres**, puis cliquez sur hello **utilisateurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="12820-211">In hello navigation pane on hello left, click **Settings**, and then click hello **Users** tab.</span></span>
   
    ![Créer un utilisateur Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_09.png)

3. <span data-ttu-id="12820-213">Cliquez sur **Add User**.</span><span class="sxs-lookup"><span data-stu-id="12820-213">Click **Add User**.</span></span> 

4. <span data-ttu-id="12820-214">Sur hello **ajouter un utilisateur** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="12820-214">On hello **Add User** dialog, perform hello following steps:</span></span>
   
    ![Créer un utilisateur Flatter Files](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatter_files_10.png)

    <span data-ttu-id="12820-216">a.</span><span class="sxs-lookup"><span data-stu-id="12820-216">a.</span></span> <span data-ttu-id="12820-217">Bonjour **prénom** zone de texte, type **Brian**.</span><span class="sxs-lookup"><span data-stu-id="12820-217">In hello **First Name** textbox, type **Britta**.</span></span>
   
    <span data-ttu-id="12820-218">b.</span><span class="sxs-lookup"><span data-stu-id="12820-218">b.</span></span> <span data-ttu-id="12820-219">Bonjour **nom** zone de texte, type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="12820-219">In hello **Last Name** textbox, type **Simon**.</span></span> 
   
    <span data-ttu-id="12820-220">c.</span><span class="sxs-lookup"><span data-stu-id="12820-220">c.</span></span> <span data-ttu-id="12820-221">Bonjour **adresse de messagerie** zone de texte, tapez l’adresse de messagerie de Brian Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="12820-221">In hello **Email Address** textbox, type Britta's email address in hello Azure portal.</span></span>
   
    <span data-ttu-id="12820-222">d.</span><span class="sxs-lookup"><span data-stu-id="12820-222">d.</span></span> <span data-ttu-id="12820-223">Cliquez sur **Envoyer**.</span><span class="sxs-lookup"><span data-stu-id="12820-223">Click **Submit**.</span></span>   


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="12820-224">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="12820-224">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="12820-225">Dans cette section, vous activez Britta Simon toouse Azure l’authentification unique par l’octroi d’accéder aux fichiers de tooFlatter.</span><span class="sxs-lookup"><span data-stu-id="12820-225">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFlatter Files.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="12820-227">**tooassign Britta Simon tooFlatter fichiers, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="12820-227">**tooassign Britta Simon tooFlatter Files, perform hello following steps:**</span></span>

1. <span data-ttu-id="12820-228">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="12820-228">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="12820-230">Dans la liste des applications hello, sélectionnez **fichiers plate**.</span><span class="sxs-lookup"><span data-stu-id="12820-230">In hello applications list, select **Flatter Files**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-flatter-files-tutorial/tutorial_flatterfiles_app.png) 

3. <span data-ttu-id="12820-232">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="12820-232">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="12820-234">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="12820-234">Click **Add** button.</span></span> <span data-ttu-id="12820-235">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="12820-235">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="12820-237">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="12820-237">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="12820-238">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="12820-238">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="12820-239">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="12820-239">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="12820-240">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="12820-240">Testing single sign-on</span></span>

<span data-ttu-id="12820-241">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="12820-241">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="12820-242">Lorsque vous cliquez sur hello fichiers plate vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour fichiers plate une application.</span><span class="sxs-lookup"><span data-stu-id="12820-242">When you click hello Flatter Files tile in hello Access Panel, you should get automatically signed-on tooyour Flatter Files application.</span></span>
<span data-ttu-id="12820-243">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="12820-243">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="12820-244">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="12820-244">Additional resources</span></span>

* [<span data-ttu-id="12820-245">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="12820-245">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="12820-246">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="12820-246">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-flatter-files-tutorial/tutorial_general_203.png

