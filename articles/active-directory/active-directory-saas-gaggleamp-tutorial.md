---
title: "Didacticiel : Intégration d’Azure Active Directory à GaggleAMP | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et GaggleAMP."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9cc1a4b7-964b-406b-9e0c-05cb1a7c9856
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 9761019a79f935b6695a5ae1214c256c887df457
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-gaggleamp"></a><span data-ttu-id="53929-103">Didacticiel : Intégration d’Azure AD à GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="53929-103">Tutorial: Azure Active Directory integration with GaggleAMP</span></span>

<span data-ttu-id="53929-104">Dans ce didacticiel, vous apprendrez comment toointegrate GaggleAMP avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="53929-104">In this tutorial, you learn how toointegrate GaggleAMP with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="53929-105">Intégration GaggleAMP à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="53929-105">Integrating GaggleAMP with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="53929-106">Vous pouvez contrôler dans Azure AD qui a accès tooGaggleAMP</span><span class="sxs-lookup"><span data-stu-id="53929-106">You can control in Azure AD who has access tooGaggleAMP</span></span>
- <span data-ttu-id="53929-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooGaggleAMP (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="53929-107">You can enable your users tooautomatically get signed-on tooGaggleAMP (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="53929-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="53929-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="53929-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="53929-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53929-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="53929-110">Prerequisites</span></span>

<span data-ttu-id="53929-111">tooconfigure intégration d’Azure AD avec GaggleAMP, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="53929-111">tooconfigure Azure AD integration with GaggleAMP, you need hello following items:</span></span>

- <span data-ttu-id="53929-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="53929-112">An Azure AD subscription</span></span>
- <span data-ttu-id="53929-113">Un abonnement GaggleAMP pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="53929-113">A GaggleAMP single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="53929-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="53929-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="53929-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="53929-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="53929-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="53929-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="53929-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="53929-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="53929-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="53929-118">Scenario description</span></span>
<span data-ttu-id="53929-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="53929-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="53929-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="53929-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="53929-121">Ajout de GaggleAMP à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="53929-121">Adding GaggleAMP from hello gallery</span></span>
2. <span data-ttu-id="53929-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="53929-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-gaggleamp-from-hello-gallery"></a><span data-ttu-id="53929-123">Ajout de GaggleAMP à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="53929-123">Adding GaggleAMP from hello gallery</span></span>
<span data-ttu-id="53929-124">intégration de hello tooconfigure de GaggleAMP dans Azure AD, vous devez tooadd GaggleAMP à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="53929-124">tooconfigure hello integration of GaggleAMP into Azure AD, you need tooadd GaggleAMP from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="53929-125">**tooadd GaggleAMP à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="53929-125">**tooadd GaggleAMP from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="53929-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="53929-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="53929-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="53929-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="53929-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="53929-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="53929-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="53929-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="53929-133">Dans la zone de recherche de hello, tapez **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="53929-133">In hello search box, type **GaggleAMP**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_search.png)

5. <span data-ttu-id="53929-135">Dans le volet de résultats hello, sélectionnez **GaggleAMP**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="53929-135">In hello results panel, select **GaggleAMP**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="53929-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="53929-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="53929-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec GaggleAMP, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="53929-138">In this section, you configure and test Azure AD single sign-on with GaggleAMP based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="53929-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans GaggleAMP est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53929-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in GaggleAMP is tooa user in Azure AD.</span></span> <span data-ttu-id="53929-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans GaggleAMP doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="53929-140">In other words, a link relationship between an Azure AD user and hello related user in GaggleAMP needs toobe established.</span></span>

<span data-ttu-id="53929-141">Dans GaggleAMP, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="53929-141">In GaggleAMP, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="53929-142">tooconfigure et test Azure AD l’authentification unique avec GaggleAMP, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="53929-142">tooconfigure and test Azure AD single sign-on with GaggleAMP, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="53929-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="53929-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="53929-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53929-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="53929-145">**[Création d’un utilisateur de test GaggleAMP](#creating-a-gaggleamp-test-user)**  -toohave un équivalent de Britta Simon dans GaggleAMP est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="53929-145">**[Creating a GaggleAMP test user](#creating-a-gaggleamp-test-user)** - toohave a counterpart of Britta Simon in GaggleAMP that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="53929-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="53929-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="53929-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="53929-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="53929-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="53929-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="53929-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="53929-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your GaggleAMP application.</span></span>

<span data-ttu-id="53929-150">**tooconfigure Azure AD single sign-on avec GaggleAMP, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="53929-150">**tooconfigure Azure AD single sign-on with GaggleAMP, perform hello following steps:**</span></span>

1. <span data-ttu-id="53929-151">Bonjour portail Azure, sur hello **GaggleAMP** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="53929-151">In hello Azure portal, on hello **GaggleAMP** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="53929-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="53929-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_samlbase.png)

3. <span data-ttu-id="53929-155">Sur hello **GaggleAMP domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="53929-155">On hello **GaggleAMP Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_url.png)

     <span data-ttu-id="53929-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.gaggleamp.com`</span><span class="sxs-lookup"><span data-stu-id="53929-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.gaggleamp.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="53929-158">valeur de Hello n’est pas réelle.</span><span class="sxs-lookup"><span data-stu-id="53929-158">hello value is not real.</span></span> <span data-ttu-id="53929-159">Valeur de hello de mise à jour avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="53929-159">Update hello value with hello actual Sign-On URL.</span></span> <span data-ttu-id="53929-160">Contact [équipe de support Client de GaggleAMP](mailto:sales@gaggleamp.com) valeur hello de tooget.</span><span class="sxs-lookup"><span data-stu-id="53929-160">Contact [GaggleAMP Client support team](mailto:sales@gaggleamp.com) tooget hello value.</span></span> 
 
4. <span data-ttu-id="53929-161">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="53929-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_certificate.png) 

5. <span data-ttu-id="53929-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="53929-163">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="53929-165">Sur hello **GaggleAMP Configuration** , cliquez sur **GaggleAMP de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="53929-165">On hello **GaggleAMP Configuration** section, click **Configure GaggleAMP** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="53929-166">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="53929-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_configure.png) 

7. <span data-ttu-id="53929-168">Dans une autre instance du navigateur, accédez à toohello page SAML SSO créé pour vous par hello poignée prend en charge d’équipe (par exemple : *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span><span class="sxs-lookup"><span data-stu-id="53929-168">In another browser instance, navigate toohello SAML SSO page created for you by hello Gaggle support team (for example: *https://accounts.gaggleamp.com/saml_configurations/oXH8sQcP79dOzgFPqrMTyw/edit*).</span></span>

8. <span data-ttu-id="53929-169">Sur votre **SSO SAML** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="53929-169">On your **SAML SSO** page, perform hello following steps:</span></span>  
   
    ![Authentification unique GaggleAMP](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_06.png) 
 
    <span data-ttu-id="53929-171">a.</span><span class="sxs-lookup"><span data-stu-id="53929-171">a.</span></span> <span data-ttu-id="53929-172">Bonjour **émetteur de fournisseur d’identité** zone de texte, valeur hello coller **URL de l’émetteur** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="53929-172">In hello **Identity Provider Issuer** textbox, paste hello value of **Issuer URL** which you have copied from Azure portal.</span></span> 
 
    <span data-ttu-id="53929-173">b.</span><span class="sxs-lookup"><span data-stu-id="53929-173">b.</span></span> <span data-ttu-id="53929-174">Bonjour **URL fournisseur d’identité unique Sign-On** zone de texte, valeur hello coller **-Service URL d’authentification** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="53929-174">In hello **Identity Provider Single Sign-On URL** textbox, paste hello  value of **Single Sign-On Service URL** which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="53929-175">c.</span><span class="sxs-lookup"><span data-stu-id="53929-175">c.</span></span> <span data-ttu-id="53929-176">Cliquez sur **Enregistrer**</span><span class="sxs-lookup"><span data-stu-id="53929-176">Click **Save**</span></span>      

    <span data-ttu-id="53929-177">d.</span><span class="sxs-lookup"><span data-stu-id="53929-177">d.</span></span> <span data-ttu-id="53929-178">Envoyer hello **certificat (Base64)** certificat tooyour [équipe de support GaggleAMP](mailto:sales@gaggleamp.com).</span><span class="sxs-lookup"><span data-stu-id="53929-178">Send hello **Certificate (Base64)** certificate tooyour [GaggleAMP support team](mailto:sales@gaggleamp.com).</span></span>

> [!TIP]
> <span data-ttu-id="53929-179">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="53929-179">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="53929-180">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="53929-180">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="53929-181">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="53929-181">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="53929-182">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="53929-182">Creating an Azure AD test user</span></span>
<span data-ttu-id="53929-183">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="53929-183">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="53929-185">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="53929-185">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="53929-186">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="53929-186">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="53929-188">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="53929-188">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="53929-190">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="53929-190">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="53929-192">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="53929-192">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-gaggleamp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="53929-194">a.</span><span class="sxs-lookup"><span data-stu-id="53929-194">a.</span></span> <span data-ttu-id="53929-195">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="53929-195">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="53929-196">b.</span><span class="sxs-lookup"><span data-stu-id="53929-196">b.</span></span> <span data-ttu-id="53929-197">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="53929-197">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="53929-198">c.</span><span class="sxs-lookup"><span data-stu-id="53929-198">c.</span></span> <span data-ttu-id="53929-199">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="53929-199">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="53929-200">d.</span><span class="sxs-lookup"><span data-stu-id="53929-200">d.</span></span> <span data-ttu-id="53929-201">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="53929-201">Click **Create**.</span></span>
 
### <a name="creating-a-gaggleamp-test-user"></a><span data-ttu-id="53929-202">Création d’un utilisateur de test GaggleAMP</span><span class="sxs-lookup"><span data-stu-id="53929-202">Creating a GaggleAMP test user</span></span>

<span data-ttu-id="53929-203">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans GaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="53929-203">hello objective of this section is toocreate a user called Britta Simon in GaggleAMP.</span></span> <span data-ttu-id="53929-204">GaggleAMP prend en charge l'approvisionnement juste-à-temps, option activée par défaut.</span><span class="sxs-lookup"><span data-stu-id="53929-204">GaggleAMP supports just-in-time provisioning, which is by default enabled.</span></span>

<span data-ttu-id="53929-205">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="53929-205">There is no action item for you in this section.</span></span> <span data-ttu-id="53929-206">Un nouvel utilisateur est créé au cours d’une tentative de tooaccess GaggleAMP s’il n’existe pas encore.</span><span class="sxs-lookup"><span data-stu-id="53929-206">A new user is created during an attempt tooaccess GaggleAMP if it doesn't exist yet.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="53929-207">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="53929-207">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="53929-208">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooGaggleAMP.</span><span class="sxs-lookup"><span data-stu-id="53929-208">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGaggleAMP.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="53929-210">**tooassign Britta Simon tooGaggleAMP, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="53929-210">**tooassign Britta Simon tooGaggleAMP, perform hello following steps:**</span></span>

1. <span data-ttu-id="53929-211">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="53929-211">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="53929-213">Dans la liste des applications hello, sélectionnez **GaggleAMP**.</span><span class="sxs-lookup"><span data-stu-id="53929-213">In hello applications list, select **GaggleAMP**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-gaggleamp-tutorial/tutorial_gaggleamp_app.png) 

3. <span data-ttu-id="53929-215">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="53929-215">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="53929-217">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="53929-217">Click **Add** button.</span></span> <span data-ttu-id="53929-218">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="53929-218">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="53929-220">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="53929-220">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="53929-221">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="53929-221">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="53929-222">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="53929-222">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="53929-223">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="53929-223">Testing single sign-on</span></span>

<span data-ttu-id="53929-224">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="53929-224">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="53929-225">Lorsque vous cliquez sur mosaïque GaggleAMP hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour GaggleAMP application.</span><span class="sxs-lookup"><span data-stu-id="53929-225">When you click hello GaggleAMP tile in hello Access Panel, you should get automatically signed-on tooyour GaggleAMP application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="53929-226">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="53929-226">Additional resources</span></span>

* [<span data-ttu-id="53929-227">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53929-227">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="53929-228">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="53929-228">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-gaggleamp-tutorial/tutorial_general_203.png

