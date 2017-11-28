---
title: "Didacticiel : intégration d’Azure Active Directory à Panopto | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Panopto."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 89c88e23-93ce-4970-9baa-1104c4e8fe4a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 76b30e1cd2782bb5fba3d229378b8f82652b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-panopto"></a><span data-ttu-id="44e31-103">Didacticiel : Intégration d’Azure Active Directory à Panopto</span><span class="sxs-lookup"><span data-stu-id="44e31-103">Tutorial: Azure Active Directory integration with Panopto</span></span>

<span data-ttu-id="44e31-104">Dans ce didacticiel, vous apprendrez comment toointegrate Panopto avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="44e31-104">In this tutorial, you learn how toointegrate Panopto with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="44e31-105">Intégration de Panopto à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="44e31-105">Integrating Panopto with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="44e31-106">Vous pouvez contrôler dans Azure AD qui a accès tooPanopto</span><span class="sxs-lookup"><span data-stu-id="44e31-106">You can control in Azure AD who has access tooPanopto</span></span>
- <span data-ttu-id="44e31-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPanopto (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="44e31-107">You can enable your users tooautomatically get signed-on tooPanopto (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="44e31-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="44e31-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="44e31-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="44e31-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44e31-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="44e31-110">Prerequisites</span></span>

<span data-ttu-id="44e31-111">tooconfigure intégration d’Azure AD à Panopto, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="44e31-111">tooconfigure Azure AD integration with Panopto, you need hello following items:</span></span>

- <span data-ttu-id="44e31-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="44e31-112">An Azure AD subscription</span></span>
- <span data-ttu-id="44e31-113">Un abonnement Panopto pour lequel l’authentification unique est activée.</span><span class="sxs-lookup"><span data-stu-id="44e31-113">A Panopto single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="44e31-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="44e31-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="44e31-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="44e31-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="44e31-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="44e31-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="44e31-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44e31-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="44e31-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="44e31-118">Scenario description</span></span>
<span data-ttu-id="44e31-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="44e31-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="44e31-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="44e31-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="44e31-121">Ajout de Panopto à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="44e31-121">Adding Panopto from hello gallery</span></span>
2. <span data-ttu-id="44e31-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="44e31-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-panopto-from-hello-gallery"></a><span data-ttu-id="44e31-123">Ajout de Panopto à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="44e31-123">Adding Panopto from hello gallery</span></span>
<span data-ttu-id="44e31-124">intégration de hello tooconfigure de Panopto dans Azure AD, vous devez tooadd Panopto à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="44e31-124">tooconfigure hello integration of Panopto into Azure AD, you need tooadd Panopto from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="44e31-125">**tooadd Panopto à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="44e31-125">**tooadd Panopto from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="44e31-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="44e31-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="44e31-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="44e31-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="44e31-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="44e31-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="44e31-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="44e31-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="44e31-133">Dans la zone de recherche de hello, tapez **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="44e31-133">In hello search box, type **Panopto**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_search.png)

5. <span data-ttu-id="44e31-135">Dans le volet de résultats hello, sélectionnez **Panopto**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="44e31-135">In hello results panel, select **Panopto**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="44e31-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="44e31-137">Configuring and testing Azure AD single sign-on</span></span>

<span data-ttu-id="44e31-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Panopto avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="44e31-138">In this section, you configure and test Azure AD single sign-on with Panopto based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="44e31-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Panopto est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44e31-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Panopto is tooa user in Azure AD.</span></span> <span data-ttu-id="44e31-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Panopto doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="44e31-140">In other words, a link relationship between an Azure AD user and hello related user in Panopto needs toobe established.</span></span>

<span data-ttu-id="44e31-141">Dans Panopto, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="44e31-141">In Panopto, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="44e31-142">tooconfigure et test Azure AD l’authentification unique à Panopto, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="44e31-142">tooconfigure and test Azure AD single sign-on with Panopto, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="44e31-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="44e31-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="44e31-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="44e31-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="44e31-145">**[Création d’un utilisateur de test Panopto](#creating-a-panopto-test-user)**  -toohave un équivalent de Britta Simon dans Panopto est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="44e31-145">**[Creating a Panopto test user](#creating-a-panopto-test-user)** - toohave a counterpart of Britta Simon in Panopto that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="44e31-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="44e31-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="44e31-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="44e31-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="44e31-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="44e31-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="44e31-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Panopto.</span><span class="sxs-lookup"><span data-stu-id="44e31-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Panopto application.</span></span>

<span data-ttu-id="44e31-150">**tooconfigure Azure AD single sign-on avec Panopto, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="44e31-150">**tooconfigure Azure AD single sign-on with Panopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="44e31-151">Bonjour portail Azure, sur hello **Panopto** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="44e31-151">In hello Azure portal, on hello **Panopto** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="44e31-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="44e31-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_samlbase.png)

3. <span data-ttu-id="44e31-155">Sur hello **Panopto domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="44e31-155">On hello **Panopto Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_url.png)

    <span data-ttu-id="44e31-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<tenant-name>.panopto.com`</span><span class="sxs-lookup"><span data-stu-id="44e31-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<tenant-name>.panopto.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="44e31-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="44e31-158">This value is not real.</span></span> <span data-ttu-id="44e31-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="44e31-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="44e31-160">Contact [équipe de support Client de Panopto](mailto:support@panopto.com‎) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="44e31-160">Contact [Panopto Client support team](mailto:support@panopto.com‎) tooget this value.</span></span> 
 
4. <span data-ttu-id="44e31-161">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="44e31-161">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_certificate.png) 

5. <span data-ttu-id="44e31-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="44e31-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panopto-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="44e31-165">Sur hello **Panopto Configuration** , cliquez sur **Panopto de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="44e31-165">On hello **Panopto Configuration** section, click **Configure Panopto** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="44e31-166">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="44e31-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_configure.png) 

7. <span data-ttu-id="44e31-168">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Panopto tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="44e31-168">In a different web browser window, log in tooyour Panopto company site as an administrator.</span></span>

8. <span data-ttu-id="44e31-169">Dans la barre d’outils de hello en hello gauche, cliquez sur **système**, puis cliquez sur **fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="44e31-169">In hello toolbar on hello left, click **System**, and then click **Identity Providers**.</span></span>
   
   <span data-ttu-id="44e31-170">![Système](./media/active-directory-saas-panopto-tutorial/ic777670.png "système")</span><span class="sxs-lookup"><span data-stu-id="44e31-170">![System](./media/active-directory-saas-panopto-tutorial/ic777670.png "System")</span></span>
9. <span data-ttu-id="44e31-171">Cliquez sur **Add Provider**.</span><span class="sxs-lookup"><span data-stu-id="44e31-171">Click **Add Provider**.</span></span>
   
   <span data-ttu-id="44e31-172">![Fournisseurs d’identité](./media/active-directory-saas-panopto-tutorial/ic777671.png "fournisseurs d’identité")</span><span class="sxs-lookup"><span data-stu-id="44e31-172">![Identity Providers](./media/active-directory-saas-panopto-tutorial/ic777671.png "Identity Providers")</span></span>
   
10. <span data-ttu-id="44e31-173">Bonjour section fournisseur SAML, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="44e31-173">In hello SAML provider section, perform hello following steps:</span></span>
   
    <span data-ttu-id="44e31-174">![Configuration SaaS](./media/active-directory-saas-panopto-tutorial/ic777672.png "configuration SaaS")</span><span class="sxs-lookup"><span data-stu-id="44e31-174">![SaaS configuration](./media/active-directory-saas-panopto-tutorial/ic777672.png "SaaS configuration")</span></span>
    
    <span data-ttu-id="44e31-175">a.</span><span class="sxs-lookup"><span data-stu-id="44e31-175">a.</span></span> <span data-ttu-id="44e31-176">À partir de hello **Type de fournisseur** liste, sélectionnez **SAML20**.</span><span class="sxs-lookup"><span data-stu-id="44e31-176">From hello **Provider Type** list, select **SAML20**.</span></span>    
    
    <span data-ttu-id="44e31-177">b.</span><span class="sxs-lookup"><span data-stu-id="44e31-177">b.</span></span> <span data-ttu-id="44e31-178">Bonjour **nom de l’Instance** zone de texte, tapez un nom pour l’instance de hello.</span><span class="sxs-lookup"><span data-stu-id="44e31-178">In hello **Instance Name** textbox, type a name for hello instance.</span></span>

    <span data-ttu-id="44e31-179">c.</span><span class="sxs-lookup"><span data-stu-id="44e31-179">c.</span></span> <span data-ttu-id="44e31-180">Bonjour **Description conviviale** zone de texte, tapez une description conviviale.</span><span class="sxs-lookup"><span data-stu-id="44e31-180">In hello **Friendly Description** textbox, type a friendly description.</span></span>
    
    <span data-ttu-id="44e31-181">d.</span><span class="sxs-lookup"><span data-stu-id="44e31-181">d.</span></span> <span data-ttu-id="44e31-182">Dans **Url de Page de rebond** hello valeur de zone de texte **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="44e31-182">In **Bounce Page Url** textbox, paste hello value of **SAML Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="44e31-183">e.</span><span class="sxs-lookup"><span data-stu-id="44e31-183">e.</span></span> <span data-ttu-id="44e31-184">Bonjour **émetteur** zone de texte, valeur hello coller **ID d’entité SAML**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="44e31-184">In hello **Issuer** textbox, paste hello value of **SAML Entity ID**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="44e31-185">f.</span><span class="sxs-lookup"><span data-stu-id="44e31-185">f.</span></span> <span data-ttu-id="44e31-186">Ouvrez votre certificat codé en base 64, ce qui vous avez téléchargé à partir d’Azure hello copie portail, contenu de celui-ci dans le Presse-papiers de tooyour, et le coller ensuite toohello **clé publique** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="44e31-186">Open your base-64 encoded certificate, which you have downloaded from Azure portal, copy hello content of it in tooyour clipboard, and then paste it toohello **Public Key**  textbox.</span></span>

11. <span data-ttu-id="44e31-187">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="44e31-187">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="44e31-188">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="44e31-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="44e31-189">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="44e31-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="44e31-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="44e31-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="44e31-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="44e31-191">Creating an Azure AD test user</span></span>

<span data-ttu-id="44e31-192">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="44e31-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="44e31-194">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="44e31-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="44e31-195">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="44e31-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="44e31-197">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="44e31-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="44e31-199">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="44e31-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="44e31-201">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="44e31-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-panopto-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="44e31-203">a.</span><span class="sxs-lookup"><span data-stu-id="44e31-203">a.</span></span> <span data-ttu-id="44e31-204">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="44e31-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="44e31-205">b.</span><span class="sxs-lookup"><span data-stu-id="44e31-205">b.</span></span> <span data-ttu-id="44e31-206">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="44e31-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="44e31-207">c.</span><span class="sxs-lookup"><span data-stu-id="44e31-207">c.</span></span> <span data-ttu-id="44e31-208">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="44e31-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="44e31-209">d.</span><span class="sxs-lookup"><span data-stu-id="44e31-209">d.</span></span> <span data-ttu-id="44e31-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="44e31-210">Click **Create**.</span></span>
 
### <a name="creating-a-panopto-test-user"></a><span data-ttu-id="44e31-211">Création d’un utilisateur de test Panopto</span><span class="sxs-lookup"><span data-stu-id="44e31-211">Creating a Panopto test user</span></span>

<span data-ttu-id="44e31-212">Il n’existe aucun élément d’action pour vous tooconfigure configuration de l’utilisateur tooPanopto.</span><span class="sxs-lookup"><span data-stu-id="44e31-212">There is no action item for you tooconfigure user provisioning tooPanopto.</span></span>  
<span data-ttu-id="44e31-213">Quand un utilisateur affecté tente de toolog dans tooPanopto à l’aide du volet d’accès hello, Panopto vérifie l’existence d’un utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="44e31-213">When an assigned user tries toolog in tooPanopto using hello access panel, Panopto checks whether hello user exists.</span></span>  

<span data-ttu-id="44e31-214">Si aucun compte d’utilisateur n’est disponible, Panopto le crée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="44e31-214">If there is no user account available yet, it is automatically created by Panopto.</span></span>

>[!NOTE]
><span data-ttu-id="44e31-215">Vous pouvez utiliser n’importe quel autre Panopto utilisateur compte outil de création ou API fournie par Panopto tooprovision comptes d’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44e31-215">You can use any other Panopto user account creation tools or APIs provided by Panopto tooprovision Azure AD user accounts.</span></span>
>
>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="44e31-216">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="44e31-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="44e31-217">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPanopto.</span><span class="sxs-lookup"><span data-stu-id="44e31-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPanopto.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="44e31-219">**tooassign Britta Simon tooPanopto, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="44e31-219">**tooassign Britta Simon tooPanopto, perform hello following steps:**</span></span>

1. <span data-ttu-id="44e31-220">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="44e31-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="44e31-222">Dans la liste des applications hello, sélectionnez **Panopto**.</span><span class="sxs-lookup"><span data-stu-id="44e31-222">In hello applications list, select **Panopto**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-panopto-tutorial/tutorial_panopto_app.png) 

3. <span data-ttu-id="44e31-224">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="44e31-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="44e31-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="44e31-226">Click **Add** button.</span></span> <span data-ttu-id="44e31-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="44e31-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="44e31-229">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="44e31-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="44e31-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="44e31-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="44e31-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="44e31-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="44e31-232">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="44e31-232">Testing single sign-on</span></span>

<span data-ttu-id="44e31-233">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="44e31-233">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="44e31-234">Lorsque vous cliquez sur mosaïque Panopto hello hello volet d’accès, vous devez obtenir automatiquement page de connexion de Panopto application.</span><span class="sxs-lookup"><span data-stu-id="44e31-234">When you click hello Panopto tile in hello Access Panel, you should get automatically login page of Panopto application.</span></span>
<span data-ttu-id="44e31-235">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="44e31-235">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="44e31-236">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="44e31-236">Additional resources</span></span>

* [<span data-ttu-id="44e31-237">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44e31-237">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="44e31-238">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="44e31-238">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-panopto-tutorial/tutorial_general_203.png

