---
title: "Didacticiel : Intégration d’Azure Active Directory avec Egnyte | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory à Box."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 8c2101d4-1779-4b36-8464-5c1ff780da18
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/18/2017
ms.author: jeedes
ms.openlocfilehash: d86fa28a1e7b23474cb76c08aef8539acadaf24d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-egnyte"></a><span data-ttu-id="bae14-103">Didacticiel : Intégration d’Azure Active Directory à Egnyte</span><span class="sxs-lookup"><span data-stu-id="bae14-103">Tutorial: Azure Active Directory integration with Egnyte</span></span>

<span data-ttu-id="bae14-104">Dans ce didacticiel, vous apprendrez comment toointegrate Egnyte avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bae14-104">In this tutorial, you learn how toointegrate Egnyte with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bae14-105">Intégration d’Egnyte à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="bae14-105">Integrating Egnyte with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bae14-106">Vous pouvez contrôler dans Azure AD qui a accès tooEgnyte</span><span class="sxs-lookup"><span data-stu-id="bae14-106">You can control in Azure AD who has access tooEgnyte</span></span>
- <span data-ttu-id="bae14-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooEgnyte (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae14-107">You can enable your users tooautomatically get signed-on tooEgnyte (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bae14-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="bae14-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bae14-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bae14-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bae14-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bae14-110">Prerequisites</span></span>

<span data-ttu-id="bae14-111">tooconfigure intégration d’Azure AD à Egnyte, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bae14-111">tooconfigure Azure AD integration with Egnyte, you need hello following items:</span></span>

- <span data-ttu-id="bae14-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae14-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bae14-113">Un abonnement Egnyte pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="bae14-113">An Egnyte single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bae14-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bae14-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bae14-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="bae14-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bae14-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bae14-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bae14-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bae14-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bae14-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="bae14-118">Scenario description</span></span>
<span data-ttu-id="bae14-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="bae14-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bae14-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="bae14-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bae14-121">Ajout d’Egnyte à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bae14-121">Adding Egnyte from hello gallery</span></span>
2. <span data-ttu-id="bae14-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae14-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-egnyte-from-hello-gallery"></a><span data-ttu-id="bae14-123">Ajout d’Egnyte à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bae14-123">Adding Egnyte from hello gallery</span></span>
<span data-ttu-id="bae14-124">intégration de hello tooconfigure d’Egnyte dans Azure AD, vous devez tooadd Egnyte à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="bae14-124">tooconfigure hello integration of Egnyte into Azure AD, you need tooadd Egnyte from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bae14-125">**tooadd Egnyte à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bae14-125">**tooadd Egnyte from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bae14-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bae14-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bae14-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="bae14-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bae14-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bae14-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="bae14-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bae14-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="bae14-133">Dans la zone de recherche de hello, tapez **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="bae14-133">In hello search box, type **Egnyte**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_search.png)

5. <span data-ttu-id="bae14-135">Dans le volet de résultats hello, sélectionnez **Egnyte**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bae14-135">In hello results panel, select **Egnyte**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bae14-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae14-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bae14-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Egnyte, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="bae14-138">In this section, you configure and test Azure AD single sign-on with Egnyte based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bae14-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Egnyte est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bae14-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Egnyte is tooa user in Azure AD.</span></span> <span data-ttu-id="bae14-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Egnyte doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="bae14-140">In other words, a link relationship between an Azure AD user and hello related user in Egnyte needs toobe established.</span></span>

<span data-ttu-id="bae14-141">Dans Egnyte, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="bae14-141">In Egnyte, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bae14-142">tooconfigure et test Azure AD l’authentification unique avec Egnyte, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="bae14-142">tooconfigure and test Azure AD single sign-on with Egnyte, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bae14-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bae14-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bae14-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bae14-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bae14-145">**[Création d’un utilisateur de test Egnyte](#creating-an-egnyte-test-user)**  -toohave un équivalent de Britta Simon dans Egnyte est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bae14-145">**[Creating an Egnyte test user](#creating-an-egnyte-test-user)** - toohave a counterpart of Britta Simon in Egnyte that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bae14-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bae14-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bae14-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="bae14-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bae14-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae14-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bae14-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Egnyte.</span><span class="sxs-lookup"><span data-stu-id="bae14-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Egnyte application.</span></span>

<span data-ttu-id="bae14-150">**tooconfigure Azure AD single sign-on avec Egnyte, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bae14-150">**tooconfigure Azure AD single sign-on with Egnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="bae14-151">Bonjour portail Azure, sur hello **Egnyte** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bae14-151">In hello Azure portal, on hello **Egnyte** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="bae14-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bae14-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_samlbase.png)

3. <span data-ttu-id="bae14-155">Sur hello **Egnyte domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bae14-155">On hello **Egnyte Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_url.png)

    <span data-ttu-id="bae14-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<companyname>.egnyte.com`</span><span class="sxs-lookup"><span data-stu-id="bae14-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<companyname>.egnyte.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bae14-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="bae14-158">This value is not real.</span></span> <span data-ttu-id="bae14-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="bae14-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="bae14-160">Contact [équipe de support Client de Egnyte](https://www.egnyte.com/corp/contact_egnyte.html) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="bae14-160">Contact [Egnyte Client support team](https://www.egnyte.com/corp/contact_egnyte.html) tooget this value.</span></span> 
 
4. <span data-ttu-id="bae14-161">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bae14-161">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_certificate.png) 

5. <span data-ttu-id="bae14-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="bae14-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bae14-165">Sur hello **Egnyte Configuration** , cliquez sur **Egnyte de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="bae14-165">On hello **Egnyte Configuration** section, click **Configure Egnyte** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="bae14-166">Hello de copie **ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="bae14-166">Copy hello **SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_configure.png) 

7. <span data-ttu-id="bae14-168">Dans une fenêtre de navigateur web, ouvrez une session dans le site d’entreprise Egnyte tooyour en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="bae14-168">In a different web browser window, log in tooyour Egnyte company site as an administrator.</span></span>

8. <span data-ttu-id="bae14-169">Cliquez sur **Settings**.</span><span class="sxs-lookup"><span data-stu-id="bae14-169">Click **Settings**.</span></span>
   
   <span data-ttu-id="bae14-170">![Paramètres](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="bae14-170">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787819.png "Settings")</span></span>

9. <span data-ttu-id="bae14-171">Dans le menu de hello, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="bae14-171">In hello menu, click **Settings**.</span></span>

   <span data-ttu-id="bae14-172">![Paramètres](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Paramètres")</span><span class="sxs-lookup"><span data-stu-id="bae14-172">![Settings](./media/active-directory-saas-egnyte-tutorial/ic787820.png "Settings")</span></span>

10. <span data-ttu-id="bae14-173">Cliquez sur hello **Configuration** onglet, puis cliquez sur **sécurité**.</span><span class="sxs-lookup"><span data-stu-id="bae14-173">Click hello **Configuration** tab, and then click **Security**.</span></span>

    <span data-ttu-id="bae14-174">![Sécurité](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Sécurité")</span><span class="sxs-lookup"><span data-stu-id="bae14-174">![Security](./media/active-directory-saas-egnyte-tutorial/ic787821.png "Security")</span></span>

11. <span data-ttu-id="bae14-175">Bonjour **unique authentification** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bae14-175">In hello **Single Sign-On Authentication** section, perform hello following steps:</span></span>

    <span data-ttu-id="bae14-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span><span class="sxs-lookup"><span data-stu-id="bae14-176">![Single Sign On Authentication](./media/active-directory-saas-egnyte-tutorial/ic787822.png "Single Sign On Authentication")</span></span>   
    
    <span data-ttu-id="bae14-177">a.</span><span class="sxs-lookup"><span data-stu-id="bae14-177">a.</span></span> <span data-ttu-id="bae14-178">Pour **Single sign-on authentication**, sélectionnez **SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="bae14-178">As **Single sign-on authentication**, select **SAML 2.0**.</span></span>
   
    <span data-ttu-id="bae14-179">b.</span><span class="sxs-lookup"><span data-stu-id="bae14-179">b.</span></span> <span data-ttu-id="bae14-180">Pour **Identity provider**, sélectionnez **AzureAD**.</span><span class="sxs-lookup"><span data-stu-id="bae14-180">As **Identity provider**, select **AzureAD**.</span></span>
   
    <span data-ttu-id="bae14-181">c.</span><span class="sxs-lookup"><span data-stu-id="bae14-181">c.</span></span> <span data-ttu-id="bae14-182">Coller **SAML Sign-On URL du Service unique** copiées à partir du portail Azure hello **Identity provider login URL** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="bae14-182">Paste **SAML Single Sign-On Service URL** copied from Azure portal into hello **Identity provider login URL** textbox.</span></span>
   
    <span data-ttu-id="bae14-183">d.</span><span class="sxs-lookup"><span data-stu-id="bae14-183">d.</span></span> <span data-ttu-id="bae14-184">Coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure en hello **entity ID fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="bae14-184">Paste **SAML Entity ID** which you have copied from Azure portal into hello **Identity provider entity ID** textbox.</span></span>
      
    <span data-ttu-id="bae14-185">e.</span><span class="sxs-lookup"><span data-stu-id="bae14-185">e.</span></span> <span data-ttu-id="bae14-186">Ouvrez votre certificat codé en base 64 dans le bloc-notes téléchargé à partir du portail Azure, hello copie contenu de celui-ci dans le Presse-papiers et le coller ensuite toohello **certificat de fournisseur d’identité** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="bae14-186">Open your base-64 encoded certificate in notepad downloaded from Azure portal, copy hello content of it into your clipboard, and then paste it toohello **Identity provider certificate** textbox.</span></span>
   
    <span data-ttu-id="bae14-187">f.</span><span class="sxs-lookup"><span data-stu-id="bae14-187">f.</span></span> <span data-ttu-id="bae14-188">Pour **Default user mapping**, sélectionnez **Email address**.</span><span class="sxs-lookup"><span data-stu-id="bae14-188">As **Default user mapping**, select **Email address**.</span></span>
   
    <span data-ttu-id="bae14-189">g.</span><span class="sxs-lookup"><span data-stu-id="bae14-189">g.</span></span> <span data-ttu-id="bae14-190">Pour **Use domain-specific issuer value**, sélectionnez **disabled**.</span><span class="sxs-lookup"><span data-stu-id="bae14-190">As **Use domain-specific issuer value**, select **disabled**.</span></span>
   
    <span data-ttu-id="bae14-191">h.</span><span class="sxs-lookup"><span data-stu-id="bae14-191">h.</span></span> <span data-ttu-id="bae14-192">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bae14-192">Click **Save**.</span></span>

> [!TIP]
> <span data-ttu-id="bae14-193">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="bae14-193">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bae14-194">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="bae14-194">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bae14-195">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bae14-195">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bae14-196">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae14-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="bae14-197">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="bae14-197">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="bae14-199">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bae14-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bae14-200">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bae14-200">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bae14-202">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="bae14-202">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bae14-204">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="bae14-204">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bae14-206">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bae14-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-egnyte-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bae14-208">a.</span><span class="sxs-lookup"><span data-stu-id="bae14-208">a.</span></span> <span data-ttu-id="bae14-209">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bae14-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bae14-210">b.</span><span class="sxs-lookup"><span data-stu-id="bae14-210">b.</span></span> <span data-ttu-id="bae14-211">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bae14-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bae14-212">c.</span><span class="sxs-lookup"><span data-stu-id="bae14-212">c.</span></span> <span data-ttu-id="bae14-213">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="bae14-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bae14-214">d.</span><span class="sxs-lookup"><span data-stu-id="bae14-214">d.</span></span> <span data-ttu-id="bae14-215">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="bae14-215">Click **Create**.</span></span>
 
### <a name="creating-an-egnyte-test-user"></a><span data-ttu-id="bae14-216">Création d’un utilisateur de test Egnyte</span><span class="sxs-lookup"><span data-stu-id="bae14-216">Creating an Egnyte test user</span></span>

<span data-ttu-id="bae14-217">tooenable Azure AD les utilisateurs toolog dans tooEgnyte, vous devez les configurer dans Egnyte.</span><span class="sxs-lookup"><span data-stu-id="bae14-217">tooenable Azure AD users toolog in tooEgnyte, they must be provisioned into Egnyte.</span></span> <span data-ttu-id="bae14-218">Dans le cas de hello d’Egnyte, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="bae14-218">In hello case of Egnyte, provisioning is a manual task.</span></span>

<span data-ttu-id="bae14-219">**effectuer des comptes d’utilisateur, tooprovision hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bae14-219">**tooprovision a user accounts, perform hello following steps:**</span></span>

1. <span data-ttu-id="bae14-220">Connectez-vous à tooyour **Egnyte** site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="bae14-220">Log in tooyour **Egnyte** company site as administrator.</span></span>

2. <span data-ttu-id="bae14-221">Accédez trop**paramètres \> utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bae14-221">Go too**Settings \> Users & Groups**.</span></span>

3. <span data-ttu-id="bae14-222">Cliquez sur **ajouter un nouvel utilisateur**, puis sélectionnez hello type d’utilisateur vous souhaitez tooadd.</span><span class="sxs-lookup"><span data-stu-id="bae14-222">Click **Add New User**, and then select hello type of user you want tooadd.</span></span>
   
   <span data-ttu-id="bae14-223">![Utilisateurs](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="bae14-223">![Users](./media/active-directory-saas-egnyte-tutorial/ic787824.png "Users")</span></span>

4. <span data-ttu-id="bae14-224">Bonjour **nouvel utilisateur Standard** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bae14-224">In hello **New Standard User** section, perform hello following steps:</span></span>
   
   <span data-ttu-id="bae14-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span><span class="sxs-lookup"><span data-stu-id="bae14-225">![New Standard User](./media/active-directory-saas-egnyte-tutorial/ic787825.png "New Standard User")</span></span>   

   <span data-ttu-id="bae14-226">a.</span><span class="sxs-lookup"><span data-stu-id="bae14-226">a.</span></span> <span data-ttu-id="bae14-227">Hello de type **messagerie**, **nom d’utilisateur**et d’autres détails d’un compte Azure Active Directory valide que vous souhaitez tooprovision.</span><span class="sxs-lookup"><span data-stu-id="bae14-227">Type hello **Email**, **Username**, and other details of a valid Azure Active Directory account you want tooprovision.</span></span>
   
   <span data-ttu-id="bae14-228">b.</span><span class="sxs-lookup"><span data-stu-id="bae14-228">b.</span></span> <span data-ttu-id="bae14-229">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="bae14-229">Click **Save**.</span></span>
    
    >[!NOTE]
    ><span data-ttu-id="bae14-230">titulaire du compte Azure Active Directory Hello recevra un e-mail de notification.</span><span class="sxs-lookup"><span data-stu-id="bae14-230">hello Azure Active Directory account holder will receive a notification email.</span></span>
    >

>[!NOTE]
><span data-ttu-id="bae14-231">Vous pouvez utiliser n’importe quel autre Egnyte utilisateur compte outil de création ou API fournie par Egnyte tooprovision des comptes d’utilisateur AAD.</span><span class="sxs-lookup"><span data-stu-id="bae14-231">You can use any other Egnyte user account creation tools or APIs provided by Egnyte tooprovision AAD user accounts.</span></span>
> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bae14-232">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bae14-232">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bae14-233">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooEgnyte.</span><span class="sxs-lookup"><span data-stu-id="bae14-233">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooEgnyte.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="bae14-235">**tooassign Britta Simon tooEgnyte, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bae14-235">**tooassign Britta Simon tooEgnyte, perform hello following steps:**</span></span>

1. <span data-ttu-id="bae14-236">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bae14-236">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="bae14-238">Dans la liste des applications hello, sélectionnez **Egnyte**.</span><span class="sxs-lookup"><span data-stu-id="bae14-238">In hello applications list, select **Egnyte**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-egnyte-tutorial/tutorial_egnyte_app.png) 

3. <span data-ttu-id="bae14-240">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bae14-240">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="bae14-242">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bae14-242">Click **Add** button.</span></span> <span data-ttu-id="bae14-243">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bae14-243">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="bae14-245">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="bae14-245">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bae14-246">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bae14-246">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bae14-247">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bae14-247">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bae14-248">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="bae14-248">Testing single sign-on</span></span>

<span data-ttu-id="bae14-249">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="bae14-249">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="bae14-250">Lorsque vous cliquez sur mosaïque Egnyte hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Egnyte application.</span><span class="sxs-lookup"><span data-stu-id="bae14-250">When you click hello Egnyte tile in hello Access Panel, you should get automatically signed-on tooyour Egnyte application.</span></span>
<span data-ttu-id="bae14-251">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="bae14-251">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bae14-252">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bae14-252">Additional resources</span></span>

* [<span data-ttu-id="bae14-253">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bae14-253">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bae14-254">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="bae14-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-egnyte-tutorial/tutorial_general_203.png

