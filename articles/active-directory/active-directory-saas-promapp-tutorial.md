---
title: "Didacticiel : intégration d’Azure Active Directory à Promapp | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Promapp."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 418d0601-6e7a-4997-a683-73fa30a2cfb5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: jeedes
ms.openlocfilehash: 02de7679b0c86d7aa8cacb41762f900dbf2ff231
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-promapp"></a><span data-ttu-id="041c4-103">Didacticiel : Intégration d’Azure Active Directory à Promapp</span><span class="sxs-lookup"><span data-stu-id="041c4-103">Tutorial: Azure Active Directory integration with Promapp</span></span>

<span data-ttu-id="041c4-104">Dans ce didacticiel, vous apprendrez comment toointegrate Promapp avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="041c4-104">In this tutorial, you learn how toointegrate Promapp with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="041c4-105">Intégration Promapp à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="041c4-105">Integrating Promapp with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="041c4-106">Vous pouvez contrôler dans Azure AD qui a accès tooPromapp</span><span class="sxs-lookup"><span data-stu-id="041c4-106">You can control in Azure AD who has access tooPromapp</span></span>
- <span data-ttu-id="041c4-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooPromapp (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="041c4-107">You can enable your users tooautomatically get signed-on tooPromapp (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="041c4-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="041c4-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="041c4-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="041c4-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="041c4-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="041c4-110">Prerequisites</span></span>

<span data-ttu-id="041c4-111">tooconfigure intégration d’Azure AD avec Promapp, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="041c4-111">tooconfigure Azure AD integration with Promapp, you need hello following items:</span></span>

- <span data-ttu-id="041c4-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="041c4-112">An Azure AD subscription</span></span>
- <span data-ttu-id="041c4-113">Un abonnement Promapp pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="041c4-113">A Promapp single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="041c4-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="041c4-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="041c4-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="041c4-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="041c4-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="041c4-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="041c4-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="041c4-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="041c4-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="041c4-118">Scenario description</span></span>
<span data-ttu-id="041c4-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="041c4-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="041c4-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="041c4-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="041c4-121">Ajout de Promapp à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="041c4-121">Adding Promapp from hello gallery</span></span>
2. <span data-ttu-id="041c4-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="041c4-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-promapp-from-hello-gallery"></a><span data-ttu-id="041c4-123">Ajout de Promapp à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="041c4-123">Adding Promapp from hello gallery</span></span>
<span data-ttu-id="041c4-124">intégration de hello tooconfigure de Promapp dans Azure AD, vous devez tooadd Promapp à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="041c4-124">tooconfigure hello integration of Promapp into Azure AD, you need tooadd Promapp from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="041c4-125">**tooadd Promapp à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="041c4-125">**tooadd Promapp from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="041c4-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="041c4-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="041c4-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="041c4-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="041c4-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="041c4-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="041c4-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="041c4-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="041c4-133">Dans la zone de recherche de hello, tapez **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="041c4-133">In hello search box, type **Promapp**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_search.png)

5. <span data-ttu-id="041c4-135">Dans le volet de résultats hello, sélectionnez **Promapp**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="041c4-135">In hello results panel, select **Promapp**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="041c4-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="041c4-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="041c4-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Promapp sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="041c4-138">In this section, you configure and test Azure AD single sign-on with Promapp based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="041c4-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Promapp est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="041c4-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Promapp is tooa user in Azure AD.</span></span> <span data-ttu-id="041c4-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Promapp doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="041c4-140">In other words, a link relationship between an Azure AD user and hello related user in Promapp needs toobe established.</span></span>

<span data-ttu-id="041c4-141">Dans Promapp, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="041c4-141">In Promapp, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="041c4-142">tooconfigure et test Azure AD l’authentification unique avec Promapp, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="041c4-142">tooconfigure and test Azure AD single sign-on with Promapp, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="041c4-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="041c4-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="041c4-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="041c4-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="041c4-145">**[Création d’un utilisateur de test Promapp](#creating-a-promapp-test-user)**  -toohave un équivalent de Britta Simon dans Promapp est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="041c4-145">**[Creating a Promapp test user](#creating-a-promapp-test-user)** - toohave a counterpart of Britta Simon in Promapp that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="041c4-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="041c4-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="041c4-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="041c4-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="041c4-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="041c4-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="041c4-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Promapp.</span><span class="sxs-lookup"><span data-stu-id="041c4-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Promapp application.</span></span>

<span data-ttu-id="041c4-150">**tooconfigure Azure AD single sign-on avec Promapp, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="041c4-150">**tooconfigure Azure AD single sign-on with Promapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="041c4-151">Bonjour portail Azure, sur hello **Promapp** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="041c4-151">In hello Azure portal, on hello **Promapp** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="041c4-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="041c4-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_samlbase.png)

3. <span data-ttu-id="041c4-155">Sur hello **Promapp domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="041c4-155">On hello **Promapp Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_url.png)

    <span data-ttu-id="041c4-157">a.</span><span class="sxs-lookup"><span data-stu-id="041c4-157">a.</span></span> <span data-ttu-id="041c4-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span><span class="sxs-lookup"><span data-stu-id="041c4-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME/saml/authenticate`</span></span>

    <span data-ttu-id="041c4-159">b.</span><span class="sxs-lookup"><span data-stu-id="041c4-159">b.</span></span> <span data-ttu-id="041c4-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://DOMAINNAME.promapp.com/TENANTNAME`</span><span class="sxs-lookup"><span data-stu-id="041c4-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://DOMAINNAME.promapp.com/TENANTNAME`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="041c4-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="041c4-161">These values are not real.</span></span> <span data-ttu-id="041c4-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="041c4-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="041c4-163">Contact [équipe de support Client de Promapp](https://www.promapp.com/about-us/contact-us/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="041c4-163">Contact [Promapp Client support team](https://www.promapp.com/about-us/contact-us/) tooget these values.</span></span>

4. <span data-ttu-id="041c4-164">Sur hello **le certificat de signature SAML** , cliquez sur **Certificate(Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="041c4-164">On hello **SAML Signing Certificate** section, click **Certificate(Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_certificate.png) 

5. <span data-ttu-id="041c4-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="041c4-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-promapp-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="041c4-168">Sur hello **Promapp Configuration** , cliquez sur **Promapp de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="041c4-168">On hello **Promapp Configuration** section, click **Configure Promapp** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="041c4-169">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="041c4-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_configure.png) 

7. <span data-ttu-id="041c4-171">Site d’entreprise Promapp tooyour ouverture de session en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="041c4-171">Sign-on tooyour Promapp company site as administrator.</span></span> 

8. <span data-ttu-id="041c4-172">Dans le menu hello haut de hello, cliquez sur **Admin**.</span><span class="sxs-lookup"><span data-stu-id="041c4-172">In hello menu on hello top, click **Admin**.</span></span> 
   
    ![Authentification unique Azure AD][12]

9. <span data-ttu-id="041c4-174">Cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="041c4-174">Click **Configure**.</span></span> 
   
    ![Authentification unique Azure AD][13]

10. <span data-ttu-id="041c4-176">Sur hello **sécurité** boîte de dialogue, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="041c4-176">On hello **Security** dialog, perform hello following steps:</span></span>
   
    ![Authentification unique Azure AD][14]
    
    <span data-ttu-id="041c4-178">a.</span><span class="sxs-lookup"><span data-stu-id="041c4-178">a.</span></span> <span data-ttu-id="041c4-179">Coller **SAML Sign-On URL du Service unique**, lequel vous avez copié à partir de hello portail Azure en hello **URL de connexion de l’authentification unique** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="041c4-179">Paste **SAML Single Sign-On Service URL**, which you have copied from hello Azure portal into hello **SSO-Login URL** textbox.</span></span>
    
    <span data-ttu-id="041c4-180">b.</span><span class="sxs-lookup"><span data-stu-id="041c4-180">b.</span></span> <span data-ttu-id="041c4-181">Pour **Mode SSO (authentification unique)**, sélectionnez **Facultatif**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="041c4-181">As **SSO - Single Sign-on Mode**, select **Optional**, and then click **Save**.</span></span>

    <span data-ttu-id="041c4-182">c.</span><span class="sxs-lookup"><span data-stu-id="041c4-182">c.</span></span> <span data-ttu-id="041c4-183">Ouvrez hello téléchargé le certificat dans le bloc-notes, le contenu du certificat hello copie sans hello première ligne (---BEGIN CERTIFICATE---) et le ligne de dernière hello (---fin certificat---), collez-le dans hello **certificat x.509 de l’authentification unique** zone de texte, puis cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="041c4-183">Open hello downloaded certificate in notepad, copy hello certificate content without hello first line (-----BEGIN CERTIFICATE-----) and hello last line (-----END CERTIFICATE-----), paste it into hello **SSO-x.509 Certificate** textbox, and then click **Save**.</span></span>
        
> [!TIP]
> <span data-ttu-id="041c4-184">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="041c4-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="041c4-185">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="041c4-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="041c4-186">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="041c4-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="041c4-187">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="041c4-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="041c4-188">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="041c4-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="041c4-190">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="041c4-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="041c4-191">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="041c4-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="041c4-193">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="041c4-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="041c4-195">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="041c4-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="041c4-197">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="041c4-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-promapp-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="041c4-199">a.</span><span class="sxs-lookup"><span data-stu-id="041c4-199">a.</span></span> <span data-ttu-id="041c4-200">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="041c4-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="041c4-201">b.</span><span class="sxs-lookup"><span data-stu-id="041c4-201">b.</span></span> <span data-ttu-id="041c4-202">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="041c4-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="041c4-203">c.</span><span class="sxs-lookup"><span data-stu-id="041c4-203">c.</span></span> <span data-ttu-id="041c4-204">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="041c4-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="041c4-205">d.</span><span class="sxs-lookup"><span data-stu-id="041c4-205">d.</span></span> <span data-ttu-id="041c4-206">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="041c4-206">Click **Create**.</span></span>
 
### <a name="creating-a-promapp-test-user"></a><span data-ttu-id="041c4-207">Création d’un utilisateur de test Promapp</span><span class="sxs-lookup"><span data-stu-id="041c4-207">Creating a Promapp test user</span></span>

<span data-ttu-id="041c4-208">Hello Promapp application prend en charge juste-à-temps de configuration.</span><span class="sxs-lookup"><span data-stu-id="041c4-208">hello Promapp application supports Just-in-Time provisioning.</span></span> <span data-ttu-id="041c4-209">Cela signifie que, un compte d’utilisateur est automatiquement créé les si nécessaire au cours d’une application de hello tooaccess tentative à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="041c4-209">This means, a user account is automatically created if necessary during an attempt tooaccess hello application using hello Access Panel.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="041c4-210">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="041c4-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="041c4-211">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooPromapp.</span><span class="sxs-lookup"><span data-stu-id="041c4-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooPromapp.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="041c4-213">**tooassign Britta Simon tooPromapp, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="041c4-213">**tooassign Britta Simon tooPromapp, perform hello following steps:**</span></span>

1. <span data-ttu-id="041c4-214">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="041c4-214">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="041c4-216">Dans la liste des applications hello, sélectionnez **Promapp**.</span><span class="sxs-lookup"><span data-stu-id="041c4-216">In hello applications list, select **Promapp**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-promapp-tutorial/tutorial_promapp_app.png) 

3. <span data-ttu-id="041c4-218">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="041c4-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="041c4-220">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="041c4-220">Click **Add** button.</span></span> <span data-ttu-id="041c4-221">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="041c4-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="041c4-223">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="041c4-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="041c4-224">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="041c4-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="041c4-225">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="041c4-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="041c4-226">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="041c4-226">Testing single sign-on</span></span>

<span data-ttu-id="041c4-227">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="041c4-227">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="041c4-228">Lorsque vous cliquez sur mosaïque Promapp hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Promapp application.</span><span class="sxs-lookup"><span data-stu-id="041c4-228">When you click hello Promapp tile in hello Access Panel, you should get automatically signed-on tooyour Promapp application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="041c4-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="041c4-229">Additional resources</span></span>

* [<span data-ttu-id="041c4-230">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="041c4-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="041c4-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="041c4-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_04.png
[12]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_05.png
[13]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_06.png
[14]: ./media/active-directory-saas-promapp-tutorial/tutorial_promapp_07.png

[100]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-promapp-tutorial/tutorial_general_203.png

