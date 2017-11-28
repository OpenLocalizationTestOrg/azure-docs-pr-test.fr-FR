---
title: "Didacticiel : Intégration d’Azure Active Directory avec IdeaScale | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et IdeaScale."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e16dda6b-fdf9-43cc-9bbb-a523f085a8af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 10722b137e7565ee165e73994fd5a60b994719bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ideascale"></a><span data-ttu-id="5752d-103">Didacticiel : Intégration d’Azure Active Directory à IdeaScale</span><span class="sxs-lookup"><span data-stu-id="5752d-103">Tutorial: Azure Active Directory integration with IdeaScale</span></span>

<span data-ttu-id="5752d-104">Dans ce didacticiel, vous apprendrez comment toointegrate IdeaScale avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="5752d-104">In this tutorial, you learn how toointegrate IdeaScale with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="5752d-105">Intégration d’IdeaScale à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="5752d-105">Integrating IdeaScale with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="5752d-106">Vous pouvez contrôler dans Azure AD qui a accès tooIdeaScale</span><span class="sxs-lookup"><span data-stu-id="5752d-106">You can control in Azure AD who has access tooIdeaScale</span></span>
- <span data-ttu-id="5752d-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooIdeaScale (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-107">You can enable your users tooautomatically get signed-on tooIdeaScale (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="5752d-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="5752d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="5752d-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="5752d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5752d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="5752d-110">Prerequisites</span></span>

<span data-ttu-id="5752d-111">tooconfigure intégration d’Azure AD à IdeaScale, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="5752d-111">tooconfigure Azure AD integration with IdeaScale, you need hello following items:</span></span>

- <span data-ttu-id="5752d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="5752d-113">Un abonnement IdeaScale pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="5752d-113">An IdeaScale single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="5752d-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="5752d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="5752d-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="5752d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="5752d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="5752d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="5752d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5752d-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="5752d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="5752d-118">Scenario description</span></span>
<span data-ttu-id="5752d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="5752d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="5752d-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="5752d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="5752d-121">Ajout d’IdeaScale à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5752d-121">Adding IdeaScale from hello gallery</span></span>
2. <span data-ttu-id="5752d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ideascale-from-hello-gallery"></a><span data-ttu-id="5752d-123">Ajout d’IdeaScale à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="5752d-123">Adding IdeaScale from hello gallery</span></span>
<span data-ttu-id="5752d-124">intégration de hello tooconfigure de IdeaScale dans Azure AD, vous devez tooadd IdeaScale à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="5752d-124">tooconfigure hello integration of IdeaScale into Azure AD, you need tooadd IdeaScale from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="5752d-125">**tooadd IdeaScale à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5752d-125">**tooadd IdeaScale from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="5752d-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5752d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="5752d-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="5752d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="5752d-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5752d-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="5752d-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="5752d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="5752d-133">Dans la zone de recherche de hello, tapez **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="5752d-133">In hello search box, type **IdeaScale**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_search.png)

5. <span data-ttu-id="5752d-135">Dans le volet de résultats hello, sélectionnez **IdeaScale**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="5752d-135">In hello results panel, select **IdeaScale**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="5752d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="5752d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec IdeaScale à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="5752d-138">In this section, you configure and test Azure AD single sign-on with IdeaScale based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="5752d-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans IdeaScale est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5752d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in IdeaScale is tooa user in Azure AD.</span></span> <span data-ttu-id="5752d-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans IdeaScale doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="5752d-140">In other words, a link relationship between an Azure AD user and hello related user in IdeaScale needs toobe established.</span></span>

<span data-ttu-id="5752d-141">En l’occurrence, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="5752d-141">In IdeaScale, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="5752d-142">tooconfigure et test Azure AD l’authentification unique à IdeaScale, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="5752d-142">tooconfigure and test Azure AD single sign-on with IdeaScale, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="5752d-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="5752d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="5752d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="5752d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="5752d-145">**[Création d’un utilisateur de test IdeaScale](#creating-an-ideascale-test-user)**  -toohave un équivalent de Britta Simon dans IdeaScale est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5752d-145">**[Creating an IdeaScale test user](#creating-an-ideascale-test-user)** - toohave a counterpart of Britta Simon in IdeaScale that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="5752d-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5752d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="5752d-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="5752d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="5752d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="5752d-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application IdeaScale.</span><span class="sxs-lookup"><span data-stu-id="5752d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your IdeaScale application.</span></span>

<span data-ttu-id="5752d-150">**tooconfigure Azure AD single sign-on avec IdeaScale, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5752d-150">**tooconfigure Azure AD single sign-on with IdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="5752d-151">Bonjour portail Azure, sur hello **IdeaScale** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5752d-151">In hello Azure portal, on hello **IdeaScale** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="5752d-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="5752d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_samlbase.png)

3. <span data-ttu-id="5752d-155">Sur hello **IdeaScale domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5752d-155">On hello **IdeaScale Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_url.png)

    <span data-ttu-id="5752d-157">a.</span><span class="sxs-lookup"><span data-stu-id="5752d-157">a.</span></span> <span data-ttu-id="5752d-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.ideascale.com`</span><span class="sxs-lookup"><span data-stu-id="5752d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.ideascale.com`</span></span>

    <span data-ttu-id="5752d-159">b.</span><span class="sxs-lookup"><span data-stu-id="5752d-159">b.</span></span> <span data-ttu-id="5752d-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :</span><span class="sxs-lookup"><span data-stu-id="5752d-160">In hello **Identifier** textbox, type a URL using hello following pattern:</span></span>
    | |
    |--|
    | `http://<companyname>.ideascale.com`  |
    | `https://<companyname>.ideascale.com` |

    > [!NOTE] 
    > <span data-ttu-id="5752d-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="5752d-161">These values are not real.</span></span> <span data-ttu-id="5752d-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="5752d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="5752d-163">Contact [équipe de support Client de IdeaScale](http://support.ideascale.com/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="5752d-163">Contact [IdeaScale Client support team](http://support.ideascale.com/) tooget these values.</span></span> 
 
4. <span data-ttu-id="5752d-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="5752d-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_certificate.png) 

5. <span data-ttu-id="5752d-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="5752d-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="5752d-168">Sur hello **IdeaScale Configuration** , cliquez sur **IdeaScale de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="5752d-168">On hello **IdeaScale Configuration** section, click **Configure IdeaScale** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="5752d-169">Hello de copie **URL de déconnexion et l’ID d’entité SAML** de hello **section de référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="5752d-169">Copy hello **Sign-Out URL, and SAML Entity ID** from hello **Quick Reference section**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_configure.png) 

7. <span data-ttu-id="5752d-171">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise IdeaScale tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5752d-171">In a different web browser window, log in tooyour IdeaScale company site as an administrator.</span></span>

8. <span data-ttu-id="5752d-172">Accédez trop**paramètres de la Communauté**.</span><span class="sxs-lookup"><span data-stu-id="5752d-172">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="5752d-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span><span class="sxs-lookup"><span data-stu-id="5752d-173">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

9. <span data-ttu-id="5752d-174">Accédez trop**sécurité \> les paramètres d’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="5752d-174">Go too**Security \> Single Signon Settings**.</span></span>
   
    <span data-ttu-id="5752d-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span><span class="sxs-lookup"><span data-stu-id="5752d-175">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790848.png "Single Signon Settings")</span></span>

10. <span data-ttu-id="5752d-176">Pour **Single-Signon Type**, sélectionnez **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="5752d-176">As **Single-Signon Type**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="5752d-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span><span class="sxs-lookup"><span data-stu-id="5752d-177">![Single Signon Type](./media/active-directory-saas-ideascale-tutorial/ic790849.png "Single Signon Type")</span></span>

11. <span data-ttu-id="5752d-178">Sur hello **les paramètres d’authentification unique** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5752d-178">On hello **Single Signon Settings** dialog, perform hello following steps:</span></span>
   
    <span data-ttu-id="5752d-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span><span class="sxs-lookup"><span data-stu-id="5752d-179">![Single Signon Settings](./media/active-directory-saas-ideascale-tutorial/ic790850.png "Single Signon Settings")</span></span>
   
    <span data-ttu-id="5752d-180">a.</span><span class="sxs-lookup"><span data-stu-id="5752d-180">a.</span></span> <span data-ttu-id="5752d-181">Dans **SAML IdP Entity ID** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5752d-181">In **SAML IdP Entity ID** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5752d-182">b.</span><span class="sxs-lookup"><span data-stu-id="5752d-182">b.</span></span> <span data-ttu-id="5752d-183">Copier le contenu de hello de votre fichier de métadonnées téléchargé à partir du portail Azure et collez-le dans hello **SAML IdP Metadata** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="5752d-183">Copy hello content of your downloaded metadata file from Azure portal, and paste it into hello **SAML IdP Metadata** textbox.</span></span>

    <span data-ttu-id="5752d-184">c.</span><span class="sxs-lookup"><span data-stu-id="5752d-184">c.</span></span> <span data-ttu-id="5752d-185">Dans **Logout Success URL** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5752d-185">In **Logout Success URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="5752d-186">d.</span><span class="sxs-lookup"><span data-stu-id="5752d-186">d.</span></span> <span data-ttu-id="5752d-187">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="5752d-187">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="5752d-188">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="5752d-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="5752d-189">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="5752d-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="5752d-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="5752d-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="5752d-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="5752d-192">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="5752d-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="5752d-194">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5752d-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="5752d-195">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="5752d-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="5752d-197">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="5752d-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="5752d-199">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="5752d-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="5752d-201">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5752d-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ideascale-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="5752d-203">a.</span><span class="sxs-lookup"><span data-stu-id="5752d-203">a.</span></span> <span data-ttu-id="5752d-204">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="5752d-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="5752d-205">b.</span><span class="sxs-lookup"><span data-stu-id="5752d-205">b.</span></span> <span data-ttu-id="5752d-206">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="5752d-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="5752d-207">c.</span><span class="sxs-lookup"><span data-stu-id="5752d-207">c.</span></span> <span data-ttu-id="5752d-208">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="5752d-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="5752d-209">d.</span><span class="sxs-lookup"><span data-stu-id="5752d-209">d.</span></span> <span data-ttu-id="5752d-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="5752d-210">Click **Create**.</span></span>
 
### <a name="creating-an-ideascale-test-user"></a><span data-ttu-id="5752d-211">Création d’un utilisateur de test IdeaScale</span><span class="sxs-lookup"><span data-stu-id="5752d-211">Creating an IdeaScale test user</span></span>

<span data-ttu-id="5752d-212">tooenable Azure AD les utilisateurs toolog en l’occurrence, ils doivent être configurés dans tooIdeaScale.</span><span class="sxs-lookup"><span data-stu-id="5752d-212">tooenable Azure AD users toolog into IdeaScale, they must be provisioned in tooIdeaScale.</span></span> <span data-ttu-id="5752d-213">Dans le cas de hello d’IdeaScale, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="5752d-213">In hello case of IdeaScale, provisioning is a manual task.</span></span>

<span data-ttu-id="5752d-214">**configuration, de l’utilisateur tooconfigure effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5752d-214">**tooconfigure user provisioning, perform hello following steps:**</span></span>

1. <span data-ttu-id="5752d-215">Connectez-vous à tooyour **IdeaScale** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="5752d-215">Log in tooyour **IdeaScale** company site as administrator.</span></span>

2. <span data-ttu-id="5752d-216">Accédez trop**paramètres de la Communauté**.</span><span class="sxs-lookup"><span data-stu-id="5752d-216">Go too**Community Settings**.</span></span>
   
    <span data-ttu-id="5752d-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span><span class="sxs-lookup"><span data-stu-id="5752d-217">![Community Settings](./media/active-directory-saas-ideascale-tutorial/ic790847.png "Community Settings")</span></span>

3. <span data-ttu-id="5752d-218">Accédez trop**les paramètres de base \> membre gestion**.</span><span class="sxs-lookup"><span data-stu-id="5752d-218">Go too**Basic Settings \> Member Management**.</span></span>

4. <span data-ttu-id="5752d-219">Cliquez sur **Add Member**.</span><span class="sxs-lookup"><span data-stu-id="5752d-219">Click **Add Member**.</span></span>
   
    <span data-ttu-id="5752d-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span><span class="sxs-lookup"><span data-stu-id="5752d-220">![Member Management](./media/active-directory-saas-ideascale-tutorial/ic790852.png "Member Management")</span></span>

5. <span data-ttu-id="5752d-221">Dans la section Add New Member de hello, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="5752d-221">In hello Add New Member section, perform hello following steps:</span></span>
   
    <span data-ttu-id="5752d-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span><span class="sxs-lookup"><span data-stu-id="5752d-222">![Add New Member](./media/active-directory-saas-ideascale-tutorial/ic790853.png "Add New Member")</span></span>
   
    <span data-ttu-id="5752d-223">a.</span><span class="sxs-lookup"><span data-stu-id="5752d-223">a.</span></span> <span data-ttu-id="5752d-224">Bonjour **les adresses de messagerie** zone de texte, tapez Bonjour adresse de messagerie d’un compte AAD valide que vous souhaitez tooprovision.</span><span class="sxs-lookup"><span data-stu-id="5752d-224">In hello **Email Addresses** textbox, type hello email address of a valid AAD account you want tooprovision.</span></span>
   
    <span data-ttu-id="5752d-225">b.</span><span class="sxs-lookup"><span data-stu-id="5752d-225">b.</span></span> <span data-ttu-id="5752d-226">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="5752d-226">Click **Save Changes**.</span></span> 
   
    >[!NOTE]
    ><span data-ttu-id="5752d-227">titulaire du compte Azure Active Directory Hello Obtient un message électronique avec un compte de hello tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="5752d-227">hello Azure Active Directory account holder gets an email with a link tooconfirm hello account before it becomes active.</span></span>
      
>[!NOTE]
><span data-ttu-id="5752d-228">Vous pouvez utiliser n’importe quel autre IdeaScale utilisateur compte outil de création ou API fournie par IdeaScale tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="5752d-228">You can use any other IdeaScale user account creation tools or APIs provided by IdeaScale tooprovision AAD user accounts.</span></span>
 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="5752d-229">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="5752d-229">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="5752d-230">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooIdeaScale.</span><span class="sxs-lookup"><span data-stu-id="5752d-230">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooIdeaScale.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="5752d-232">**tooassign Britta Simon tooIdeaScale, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="5752d-232">**tooassign Britta Simon tooIdeaScale, perform hello following steps:**</span></span>

1. <span data-ttu-id="5752d-233">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="5752d-233">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="5752d-235">Dans la liste des applications hello, sélectionnez **IdeaScale**.</span><span class="sxs-lookup"><span data-stu-id="5752d-235">In hello applications list, select **IdeaScale**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ideascale-tutorial/tutorial_ideascale_app.png) 

3. <span data-ttu-id="5752d-237">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5752d-237">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="5752d-239">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="5752d-239">Click **Add** button.</span></span> <span data-ttu-id="5752d-240">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5752d-240">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="5752d-242">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="5752d-242">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="5752d-243">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="5752d-243">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="5752d-244">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="5752d-244">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="5752d-245">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="5752d-245">Testing single sign-on</span></span>


<span data-ttu-id="5752d-246">objectif Hello de cette section est tootest votre configuration de l’authentification unique Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="5752d-246">hello objective of this section is tootest your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="5752d-247">Lorsque vous cliquez sur mosaïque IdeaScale hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour IdeaScale application.</span><span class="sxs-lookup"><span data-stu-id="5752d-247">When you click hello IdeaScale tile in hello Access Panel, you should get automatically signed-on tooyour IdeaScale application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5752d-248">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="5752d-248">Additional resources</span></span>

* [<span data-ttu-id="5752d-249">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5752d-249">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="5752d-250">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="5752d-250">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ideascale-tutorial/tutorial_general_203.png

