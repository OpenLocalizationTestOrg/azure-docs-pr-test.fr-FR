---
title: "Tutoriel : Intégration d’Azure Active Directory à Menlo Security | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et la sécurité de Menlo."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 9e63fe6b-0ad0-405d-9e41-6a1a40a41df8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: jeedes
ms.openlocfilehash: 193d12eedf31f4f08e1d141936d6e918c36a2109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-menlo-security"></a><span data-ttu-id="89328-103">Tutoriel : Intégration d’Azure Active Directory à Menlo Security</span><span class="sxs-lookup"><span data-stu-id="89328-103">Tutorial: Azure Active Directory integration with Menlo Security</span></span>

<span data-ttu-id="89328-104">Dans ce didacticiel, vous apprendrez comment toointegrate sécurité Menlo avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89328-104">In this tutorial, you learn how toointegrate Menlo Security with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="89328-105">Intégration de sécurité de Menlo avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="89328-105">Integrating Menlo Security with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="89328-106">Vous pouvez contrôler dans Azure AD qui a accès tooMenlo sécurité</span><span class="sxs-lookup"><span data-stu-id="89328-106">You can control in Azure AD who has access tooMenlo Security</span></span>
- <span data-ttu-id="89328-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooMenlo sécurité (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="89328-107">You can enable your users tooautomatically get signed-on tooMenlo Security (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="89328-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="89328-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="89328-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez.</span><span class="sxs-lookup"><span data-stu-id="89328-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="89328-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="89328-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89328-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="89328-111">Prerequisites</span></span>

<span data-ttu-id="89328-112">tooconfigure intégration d’Azure AD avec Menlo de sécurité, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="89328-112">tooconfigure Azure AD integration with Menlo Security, you need hello following items:</span></span>

- <span data-ttu-id="89328-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="89328-113">An Azure AD subscription</span></span>
- <span data-ttu-id="89328-114">Un abonnement Menlo Security pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="89328-114">A Menlo Security single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="89328-115">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="89328-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="89328-116">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="89328-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="89328-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="89328-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="89328-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="89328-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="89328-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="89328-119">Scenario description</span></span>
<span data-ttu-id="89328-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="89328-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="89328-121">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="89328-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="89328-122">Ajout de Menlo sécurité à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="89328-122">Adding Menlo Security from hello gallery</span></span>
2. <span data-ttu-id="89328-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="89328-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-menlo-security-from-hello-gallery"></a><span data-ttu-id="89328-124">Ajout de Menlo sécurité à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="89328-124">Adding Menlo Security from hello gallery</span></span>
<span data-ttu-id="89328-125">tooconfigure hello intégration de sécurité de Menlo dans Azure AD, vous devez tooadd Menlo sécurité à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="89328-125">tooconfigure hello integration of Menlo Security into Azure AD, you need tooadd Menlo Security from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="89328-126">**tooadd sécurité Menlo à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="89328-126">**tooadd Menlo Security from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="89328-127">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="89328-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="89328-129">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="89328-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="89328-130">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="89328-130">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="89328-132">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="89328-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="89328-134">Dans la zone de recherche de hello, tapez **Menlo sécurité**.</span><span class="sxs-lookup"><span data-stu-id="89328-134">In hello search box, type **Menlo Security**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_search.png)

5. <span data-ttu-id="89328-136">Dans le volet de résultats hello, sélectionnez **Menlo sécurité**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="89328-136">In hello results panel, select **Menlo Security**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="89328-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="89328-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="89328-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Menlo Security, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="89328-139">In this section, you configure and test Azure AD single sign-on with Menlo Security based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="89328-140">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent de hello en mode de sécurité Menlo est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89328-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Menlo Security is tooa user in Azure AD.</span></span> <span data-ttu-id="89328-141">En d’autres termes, une relation de lien entre un utilisateur Azure AD et l’utilisateur en mode de sécurité Menlo hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="89328-141">In other words, a link relationship between an Azure AD user and hello related user in Menlo Security needs toobe established.</span></span>

<span data-ttu-id="89328-142">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** Menlo sécurité.</span><span class="sxs-lookup"><span data-stu-id="89328-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Menlo Security.</span></span>

<span data-ttu-id="89328-143">tooconfigure et test Azure AD l’authentification unique avec Menlo de sécurité, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="89328-143">tooconfigure and test Azure AD single sign-on with Menlo Security, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="89328-144">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="89328-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="89328-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="89328-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="89328-146">**[Création d’un utilisateur de test Menlo sécurité](#creating-a-menlo-security-test-user)**  -toohave un équivalent de Britta Simon dans sécurité Menlo qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="89328-146">**[Creating a Menlo Security test user](#creating-a-menlo-security-test-user)** - toohave a counterpart of Britta Simon in Menlo Security that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="89328-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="89328-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="89328-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="89328-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="89328-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="89328-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="89328-150">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Menlo sécurité.</span><span class="sxs-lookup"><span data-stu-id="89328-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Menlo Security application.</span></span>

<span data-ttu-id="89328-151">**tooconfigure Azure AD single sign-on avec Menlo sécurité, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="89328-151">**tooconfigure Azure AD single sign-on with Menlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="89328-152">Bonjour portail Azure, sur hello **Menlo sécurité** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="89328-152">In hello Azure portal, on hello **Menlo Security** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="89328-154">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="89328-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_samlbase.png)

3. <span data-ttu-id="89328-156">Sur hello **URL et le domaine de sécurité Menlo** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="89328-156">On hello **Menlo Security Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_url.png)

    <span data-ttu-id="89328-158">a.</span><span class="sxs-lookup"><span data-stu-id="89328-158">a.</span></span> <span data-ttu-id="89328-159">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.menlosecurity.com/account/login`</span><span class="sxs-lookup"><span data-stu-id="89328-159">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/account/login`</span></span>

    <span data-ttu-id="89328-160">b.</span><span class="sxs-lookup"><span data-stu-id="89328-160">b.</span></span> <span data-ttu-id="89328-161">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span><span class="sxs-lookup"><span data-stu-id="89328-161">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<subdomain>.menlosecurity.com/safeview-auth-server/saml/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="89328-162">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="89328-162">These values are not hello real.</span></span> <span data-ttu-id="89328-163">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="89328-163">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="89328-164">Contact [équipe de support Client de sécurité Menlo](https://www.menlosecurity.com/menlo-contact) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="89328-164">Contact [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooget these values.</span></span> 
 
4. <span data-ttu-id="89328-165">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="89328-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello Certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_certificate.png) 

5. <span data-ttu-id="89328-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="89328-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="89328-169">Sur hello **Configuration de la sécurité Menlo** , cliquez sur **configurer la sécurité Menlo** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="89328-169">On hello **Menlo Security Configuration** section, click **Configure Menlo Security** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="89328-170">Hello de copie **ID d’entité SAML**, et **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="89328-170">Copy hello **SAML Entity ID**, and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_configure.png) 

7. <span data-ttu-id="89328-172">tooconfigure l’authentification unique sur **Menlo sécurité** côté, connexion toohello **Menlo sécurité** site Web en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="89328-172">tooconfigure single sign-on on **Menlo Security** side, login toohello **Menlo Security** website as an administrator.</span></span>

8. <span data-ttu-id="89328-173">Sous **paramètres** accédez trop**authentification** et procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="89328-173">Under **Settings** go too**Authentication** and perform following actions:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/menlo_user_setup.png)

    <span data-ttu-id="89328-175">a.</span><span class="sxs-lookup"><span data-stu-id="89328-175">a.</span></span> <span data-ttu-id="89328-176">Cochez la case à cocher hello **activer l’authentification d’utilisateur à l’aide de SAML**.</span><span class="sxs-lookup"><span data-stu-id="89328-176">Tick hello checkbox **Enable user authentication using SAML**.</span></span>

    <span data-ttu-id="89328-177">b.</span><span class="sxs-lookup"><span data-stu-id="89328-177">b.</span></span> <span data-ttu-id="89328-178">Sélectionnez **autoriser l’accès externe** trop**Oui**.</span><span class="sxs-lookup"><span data-stu-id="89328-178">Select **Allow External Access** too**Yes**.</span></span>

    <span data-ttu-id="89328-179">c.</span><span class="sxs-lookup"><span data-stu-id="89328-179">c.</span></span> <span data-ttu-id="89328-180">Sous **SAML Provider**, sélectionnez **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="89328-180">Under **SAML Provider**, select **Azure Active Directory**.</span></span>

    <span data-ttu-id="89328-181">d.</span><span class="sxs-lookup"><span data-stu-id="89328-181">d.</span></span> <span data-ttu-id="89328-182">**Le point de terminaison SAML 2.0** : hello de coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="89328-182">**SAML 2.0 Endpoint** : Paste hello **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="89328-183">e.</span><span class="sxs-lookup"><span data-stu-id="89328-183">e.</span></span> <span data-ttu-id="89328-184">**Identificateur de service (émetteur)** : hello de coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="89328-184">**Service Identifier (Issuer)** : Paste hello **SAML Entity ID** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="89328-185">f.</span><span class="sxs-lookup"><span data-stu-id="89328-185">f.</span></span> <span data-ttu-id="89328-186">**Certificat X.509** : hello ouvrir **certificat (Base64)** téléchargé à partir de hello portail Azure dans le bloc-notes et collez-le dans cette zone.</span><span class="sxs-lookup"><span data-stu-id="89328-186">**X.509 Certificate** : Open hello **Certificate (Base64)** downloaded from hello Azure Portal in notepad and paste it in this box.</span></span>

    <span data-ttu-id="89328-187">g.</span><span class="sxs-lookup"><span data-stu-id="89328-187">g.</span></span> <span data-ttu-id="89328-188">Cliquez sur **enregistrer** toosave les paramètres hello.</span><span class="sxs-lookup"><span data-stu-id="89328-188">Click **Save** toosave hello settings.</span></span>

> [!TIP]
> <span data-ttu-id="89328-189">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="89328-189">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="89328-190">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="89328-190">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="89328-191">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="89328-191">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="89328-192">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="89328-192">Creating an Azure AD test user</span></span>
<span data-ttu-id="89328-193">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="89328-193">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="89328-195">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="89328-195">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="89328-196">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="89328-196">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="89328-198">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="89328-198">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="89328-200">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="89328-200">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="89328-202">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="89328-202">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-menlosecurity-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="89328-204">a.</span><span class="sxs-lookup"><span data-stu-id="89328-204">a.</span></span> <span data-ttu-id="89328-205">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="89328-205">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="89328-206">b.</span><span class="sxs-lookup"><span data-stu-id="89328-206">b.</span></span> <span data-ttu-id="89328-207">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="89328-207">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="89328-208">c.</span><span class="sxs-lookup"><span data-stu-id="89328-208">c.</span></span> <span data-ttu-id="89328-209">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="89328-209">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="89328-210">d.</span><span class="sxs-lookup"><span data-stu-id="89328-210">d.</span></span> <span data-ttu-id="89328-211">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="89328-211">Click **Create**.</span></span>
 
### <a name="creating-a-menlo-security-test-user"></a><span data-ttu-id="89328-212">Création d’un utilisateur de test Menlo Security</span><span class="sxs-lookup"><span data-stu-id="89328-212">Creating a Menlo Security test user</span></span>
 
<span data-ttu-id="89328-213">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Menlo Security.</span><span class="sxs-lookup"><span data-stu-id="89328-213">In this section, you create a user called Britta Simon in Menlo Security.</span></span> <span data-ttu-id="89328-214">Travailler avec [équipe de support Client de sécurité Menlo](https://www.menlosecurity.com/menlo-contact) utilisateurs hello tooadd hello Menlo Security platform.</span><span class="sxs-lookup"><span data-stu-id="89328-214">Work with [Menlo Security Client support team](https://www.menlosecurity.com/menlo-contact) tooadd hello users in hello Menlo Security platform.</span></span> <span data-ttu-id="89328-215">Les utilisateurs doivent être créés et activés avant que vous utilisiez l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="89328-215">Users must be created and activated before you use single sign-on.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="89328-216">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="89328-216">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="89328-217">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooMenlo sécurité.</span><span class="sxs-lookup"><span data-stu-id="89328-217">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooMenlo Security.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="89328-219">**tooassign Britta Simon tooMenlo sécurité, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="89328-219">**tooassign Britta Simon tooMenlo Security, perform hello following steps:**</span></span>

1. <span data-ttu-id="89328-220">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="89328-220">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="89328-222">Dans la liste des applications hello, sélectionnez **Menlo sécurité**.</span><span class="sxs-lookup"><span data-stu-id="89328-222">In hello applications list, select **Menlo Security**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-menlosecurity-tutorial/tutorial_menlosecurity_app.png) 

3. <span data-ttu-id="89328-224">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="89328-224">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="89328-226">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="89328-226">Click **Add** button.</span></span> <span data-ttu-id="89328-227">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="89328-227">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="89328-229">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="89328-229">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="89328-230">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="89328-230">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="89328-231">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="89328-231">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="89328-232">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="89328-232">Testing single sign-on</span></span>

<span data-ttu-id="89328-233">Dans cette section, vous allez tester la configuration de l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89328-233">In this section, you test your Azure AD single sign-on configuration.</span></span>

<span data-ttu-id="89328-234">Ouvrez une fenêtre de navigateur dans un mode « Navigation InPrivate » ou « Incognito » tootrigger une nouvelle authentification.</span><span class="sxs-lookup"><span data-stu-id="89328-234">Open a browser window in an "InPrivate" or "Incognito" mode tootrigger a new authentication.</span></span>  <span data-ttu-id="89328-235">Dans Internet Explorer, utilisez Ctrl+Maj+P.</span><span class="sxs-lookup"><span data-stu-id="89328-235">In Internet Explorer, use Ctrl+Shift+P.</span></span>  <span data-ttu-id="89328-236">Dans Chrome, utilisez Ctrl+Maj+N.</span><span class="sxs-lookup"><span data-stu-id="89328-236">In Chrome, use Ctrl+Shift+N.</span></span>  <span data-ttu-id="89328-237">Dans la fenêtre de navigation privée hello, tooa de parcourir une ressource protégée et d’effectuer une connexion d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="89328-237">In hello private browsing window, browse tooa protected resource and perform an Azure AD login.</span></span>  <span data-ttu-id="89328-238">Dès la connexion établie, vous serez site demandé de toohello prises dans une session d’isolation.</span><span class="sxs-lookup"><span data-stu-id="89328-238">Upon successful login, you will be taken toohello requested site in an isolation session.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="89328-239">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="89328-239">Additional resources</span></span>

* [<span data-ttu-id="89328-240">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="89328-240">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="89328-241">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="89328-241">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-menlosecurity-tutorial/tutorial_general_203.png

