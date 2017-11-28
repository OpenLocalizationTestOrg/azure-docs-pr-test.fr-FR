---
title: "Didacticiel : intégration d’Azure Active Directory à Google Apps dans Azure | Documents Microsoft"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Google Apps."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 38a6ca75-7fd0-4cdc-9b9f-fae080c5a016
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 2093b5ab605ec0d7bbefe7a78e1eede34d756f53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-google-apps"></a><span data-ttu-id="112c2-103">Didacticiel : Intégration d’Azure Active Directory à Google Apps</span><span class="sxs-lookup"><span data-stu-id="112c2-103">Tutorial: Azure Active Directory integration with Google Apps</span></span>

<span data-ttu-id="112c2-104">Dans ce didacticiel, vous apprendrez comment toointegrate Google Apps avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="112c2-104">In this tutorial, you learn how toointegrate Google Apps with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="112c2-105">Intégration de Google Apps à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="112c2-105">Integrating Google Apps with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="112c2-106">Vous pouvez contrôler dans Azure AD qui a accès tooGoogle applications</span><span class="sxs-lookup"><span data-stu-id="112c2-106">You can control in Azure AD who has access tooGoogle Apps</span></span>
- <span data-ttu-id="112c2-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooGoogle (Single Sign-On), les applications avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="112c2-107">You can enable your users tooautomatically get signed-on tooGoogle Apps (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="112c2-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="112c2-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="112c2-109">Si vous souhaitez tooknow plus d’informations sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="112c2-109">If you want tooknow more information about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="112c2-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="112c2-110">Prerequisites</span></span>

<span data-ttu-id="112c2-111">tooconfigure intégration d’Azure AD à Google Apps, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="112c2-111">tooconfigure Azure AD integration with Google Apps, you need hello following items:</span></span>

- <span data-ttu-id="112c2-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="112c2-112">An Azure AD subscription</span></span>
- <span data-ttu-id="112c2-113">Un abonnement Google pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="112c2-113">A Google Apps single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="112c2-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="112c2-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="112c2-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="112c2-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="112c2-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="112c2-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="112c2-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez bénéficier de l’essai d’un mois ici : [Offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="112c2-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="video-tutorial"></a><span data-ttu-id="112c2-118">Didacticiel vidéo</span><span class="sxs-lookup"><span data-stu-id="112c2-118">Video tutorial</span></span>
<span data-ttu-id="112c2-119">Comment tooEnable Single Sign-On tooGoogle des applications dans les 2 Minutes :</span><span class="sxs-lookup"><span data-stu-id="112c2-119">How tooEnable Single Sign-On tooGoogle Apps in 2 Minutes:</span></span>

> [!VIDEO https://channel9.msdn.com/Series/Azure-Active-Directory-Videos-Demos/Enable-single-sign-on-to-Google-Apps-in-2-minutes-with-Azure-AD/player]

## <a name="frequently-asked-questions"></a><span data-ttu-id="112c2-120">Forum Aux Questions (FAQ)</span><span class="sxs-lookup"><span data-stu-id="112c2-120">Frequently Asked Questions</span></span>
1. <span data-ttu-id="112c2-121">**Q : Les Chromebooks et les autres appareils Chrome sont-ils compatibles avec l’authentification unique Azure AD ?**</span><span class="sxs-lookup"><span data-stu-id="112c2-121">**Q: Are Chromebooks and other Chrome devices compatible with Azure AD single sign-on?**</span></span>
   
    <span data-ttu-id="112c2-122">R : Oui, les utilisateurs sont en mesure de toosign dans leurs appareils Chromebook à l’aide de leurs informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="112c2-122">A: Yes, users are able toosign into their Chromebook devices using their Azure AD credentials.</span></span> <span data-ttu-id="112c2-123">Consultez cet [article du support technique Google Apps](https://support.google.com/chrome/a/answer/6060880) pour en savoir plus sur les raisons de la double demande de saisie des informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="112c2-123">See this [Google Apps support article](https://support.google.com/chrome/a/answer/6060880) for information on why users may get prompted for credentials twice.</span></span>

2. <span data-ttu-id="112c2-124">**Q : si j’activer l’authentification unique, les utilisateurs de s’être toouse en mesure de leur toosign d’informations d’identification Azure AD dans tous les produits Google, telles que la classe de Google, GMail, Google Drive, YouTube et ainsi de suite ?**</span><span class="sxs-lookup"><span data-stu-id="112c2-124">**Q: If I enable single sign-on, will users be able toouse their Azure AD credentials toosign into any Google product, such as Google Classroom, GMail, Google Drive, YouTube, and so on?**</span></span>
   
    <span data-ttu-id="112c2-125">R : Oui, en fonction de [les applications de Google](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) vous choisissez tooenable ou désactiver pour votre organisation.</span><span class="sxs-lookup"><span data-stu-id="112c2-125">A: Yes, depending on [which Google apps](https://support.google.com/a/answer/182442?hl=en&ref_topic=1227583) you choose tooenable or disable for your organization.</span></span>

3. <span data-ttu-id="112c2-126">**Q : Puis-je activer l’authentification unique pour uniquement un sous-ensemble de mes utilisateurs Google Apps ?**</span><span class="sxs-lookup"><span data-stu-id="112c2-126">**Q: Can I enable single sign-on for only a subset of my Google Apps users?**</span></span>
   
    <span data-ttu-id="112c2-127">R : non, activer l’authentification unique sur immédiatement nécessite tous les votre tooauthenticate d’utilisateurs de Google Apps avec leurs informations d’identification Azure AD.</span><span class="sxs-lookup"><span data-stu-id="112c2-127">A: No, turning on single sign-on immediately requires all your Google Apps users tooauthenticate with their Azure AD credentials.</span></span> <span data-ttu-id="112c2-128">Étant donné que Google Apps ne prend en charge plusieurs fournisseurs d’identité, le fournisseur d’identité pour votre environnement de Google Apps hello peut être Azure AD ou Google--mais pas les deux à hello même temps.</span><span class="sxs-lookup"><span data-stu-id="112c2-128">Because Google Apps doesn't support having multiple identity providers, hello identity provider for your Google Apps environment can either be Azure AD or Google -- but not both at hello same time.</span></span>

4. <span data-ttu-id="112c2-129">**Q : si un utilisateur est connecté via Windows, sont qu'elles authentifient automatiquement les applications tooGoogle sans mise en route invité à entrer un mot de passe ?**</span><span class="sxs-lookup"><span data-stu-id="112c2-129">**Q: If a user is signed in through Windows, are they automatically authenticate tooGoogle Apps without getting prompted for a password?**</span></span>
   
    <span data-ttu-id="112c2-130">R : Ce scénario peut être activé par le biais de deux options.</span><span class="sxs-lookup"><span data-stu-id="112c2-130">A: There are two options for enabling this scenario.</span></span> <span data-ttu-id="112c2-131">Tout d’abord, les utilisateurs peuvent se connecter aux appareils Windows 10 via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="112c2-131">First, users could sign into Windows 10 devices via [Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span> <span data-ttu-id="112c2-132">Vous pouvez également les utilisateurs pourraient s’appareils Windows, qui sont joints au domaine de tooan locale Active Directory qui a été activé pour une seule session tooAzure AD via un [les Services de fédération Active Directory (AD FS)](active-directory-aadconnect-user-signin.md) déploiement.</span><span class="sxs-lookup"><span data-stu-id="112c2-132">Alternatively, users could sign into Windows devices that are domain-joined tooan on-premises Active Directory that has been enabled for single sign-on tooAzure AD via an [Active Directory Federation Services (AD FS)](active-directory-aadconnect-user-signin.md) deployment.</span></span> <span data-ttu-id="112c2-133">Les deux options nécessitent un tooperform les étapes de hello Bonjour suivant didacticiel tooenable l’authentification unique entre Azure AD et Google Apps.</span><span class="sxs-lookup"><span data-stu-id="112c2-133">Both options require you tooperform hello steps in hello following tutorial tooenable single sign-on between Azure AD and Google Apps.</span></span>

## <a name="scenario-description"></a><span data-ttu-id="112c2-134">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="112c2-134">Scenario description</span></span>
<span data-ttu-id="112c2-135">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="112c2-135">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="112c2-136">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="112c2-136">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="112c2-137">Ajout de Google Apps à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="112c2-137">Adding Google Apps from hello gallery</span></span>
2. <span data-ttu-id="112c2-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="112c2-138">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-google-apps-from-hello-gallery"></a><span data-ttu-id="112c2-139">Ajout de Google Apps à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="112c2-139">Adding Google Apps from hello gallery</span></span>
<span data-ttu-id="112c2-140">tooconfigure hello intégration de Google Apps dans Azure AD, vous devez tooadd Google Apps à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="112c2-140">tooconfigure hello integration of Google Apps into Azure AD, you need tooadd Google Apps from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="112c2-141">**tooadd Google Apps à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="112c2-141">**tooadd Google Apps from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="112c2-142">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="112c2-142">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="112c2-144">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="112c2-144">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="112c2-145">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="112c2-145">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="112c2-147">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="112c2-147">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="112c2-149">Dans la zone de recherche de hello, tapez **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="112c2-149">In hello search box, type **Google Apps**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_search.png)

5. <span data-ttu-id="112c2-151">Dans le volet de résultats hello, sélectionnez **Google Apps**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="112c2-151">In hello results panel, select **Google Apps**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="112c2-153">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="112c2-153">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="112c2-154">Dans cette section, configurez et testez l’authentification unique Azure AD avec Google Apps sur un utilisateur test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="112c2-154">In this section, you configure and test Azure AD single sign-on with Google Apps based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="112c2-155">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Google Apps est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="112c2-155">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Google Apps is tooa user in Azure AD.</span></span> <span data-ttu-id="112c2-156">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Google Apps doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="112c2-156">In other words, a link relationship between an Azure AD user and hello related user in Google Apps needs toobe established.</span></span>

<span data-ttu-id="112c2-157">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Google Apps.</span><span class="sxs-lookup"><span data-stu-id="112c2-157">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Google Apps.</span></span>

<span data-ttu-id="112c2-158">tooconfigure et test Azure AD l’authentification unique avec Google Apps, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="112c2-158">tooconfigure and test Azure AD single sign-on with Google Apps, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="112c2-159">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="112c2-159">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="112c2-160">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="112c2-160">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="112c2-161">**[Création d’un utilisateur de test de Google Apps](#creating-a-google-apps-test-user)**  -toohave un équivalent de Britta Simon dans Google Apps qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="112c2-161">**[Creating a Google Apps test user](#creating-a-google-apps-test-user)** - toohave a counterpart of Britta Simon in Google Apps that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="112c2-162">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="112c2-162">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="112c2-163">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="112c2-163">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="112c2-164">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="112c2-164">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="112c2-165">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Google Apps.</span><span class="sxs-lookup"><span data-stu-id="112c2-165">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Google Apps application.</span></span>

<span data-ttu-id="112c2-166">**tooconfigure Azure AD single sign-on avec Google Apps, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="112c2-166">**tooconfigure Azure AD single sign-on with Google Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="112c2-167">Bonjour portail Azure, sur hello **Google Apps** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="112c2-167">In hello Azure portal, on hello **Google Apps** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="112c2-169">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="112c2-169">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_samlbase.png)

3. <span data-ttu-id="112c2-171">Sur hello **URL et le domaine Google Apps** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="112c2-171">On hello **Google Apps Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_url.png)

    <span data-ttu-id="112c2-173">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://mail.google.com/a/<yourdomain>`</span><span class="sxs-lookup"><span data-stu-id="112c2-173">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://mail.google.com/a/<yourdomain>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="112c2-174">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="112c2-174">This value is not real.</span></span> <span data-ttu-id="112c2-175">Mettre à jour la valeur de hello avec l’URL de connexion réel hello.</span><span class="sxs-lookup"><span data-stu-id="112c2-175">Update hello value with hello actual Sign-on URL.</span></span> <span data-ttu-id="112c2-176">Contactez hello [équipe de support technique de Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="112c2-176">contact hello [Google support team](https://www.google.com/contact/).</span></span>
 
4. <span data-ttu-id="112c2-177">Sur hello **le certificat de signature SAML** , cliquez sur **certificat** , puis enregistrez le certificat de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="112c2-177">On hello **SAML Signing Certificate** section, click **Certificate** and then save hello certificate on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_certificate.png) 

5. <span data-ttu-id="112c2-179">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="112c2-179">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="112c2-181">Sur hello **Google Apps Configuration** , cliquez sur **configurer Google Apps** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="112c2-181">On hello **Google Apps Configuration** section, click **Configure Google Apps** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="112c2-182">Hello de copie **URL de déconnexion, SAML Sign-On URL du Service unique et modifier une URL de mot de passe** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="112c2-182">Copy hello **Sign-Out URL, SAML Single Sign-On Service URL and Change password URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_configure.png) 

7. <span data-ttu-id="112c2-184">Ouvrez un nouvel onglet dans votre navigateur et connectez-vous à hello [Google Apps Admin Console](http://admin.google.com/) à l’aide de votre compte d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="112c2-184">Open a new tab in your browser, and sign into hello [Google Apps Admin Console](http://admin.google.com/) using your administrator account.</span></span>

8. <span data-ttu-id="112c2-185">Cliquez sur **Security**.</span><span class="sxs-lookup"><span data-stu-id="112c2-185">Click **Security**.</span></span> <span data-ttu-id="112c2-186">Si vous ne voyez pas le lien de hello, il peut être masquée sous hello **plus de contrôles** menu bas hello écran hello.</span><span class="sxs-lookup"><span data-stu-id="112c2-186">If you don't see hello link, it may be hidden under hello **More Controls** menu at hello bottom of hello screen.</span></span>
   
    ![Cliquez sur Sécurité.][10]

9. <span data-ttu-id="112c2-188">Sur hello **sécurité** , cliquez sur **configurer l’authentification unique (SSO).**</span><span class="sxs-lookup"><span data-stu-id="112c2-188">On hello **Security** page, click **Set up single sign-on (SSO).**</span></span>
   
    ![Cliquez sur Authentification unique.][11]

10. <span data-ttu-id="112c2-190">Effectuez hello les modifications de configuration suivantes :</span><span class="sxs-lookup"><span data-stu-id="112c2-190">Perform hello following configuration changes:</span></span>
   
    ![Configurer l’authentification unique][12]
   
    <span data-ttu-id="112c2-192">a.</span><span class="sxs-lookup"><span data-stu-id="112c2-192">a.</span></span> <span data-ttu-id="112c2-193">Sélectionnez **Configurer l'authentification unique avec un fournisseur d'identité tiers**.</span><span class="sxs-lookup"><span data-stu-id="112c2-193">Select **Setup SSO with third-party identity provider**.</span></span>

    <span data-ttu-id="112c2-194">b.</span><span class="sxs-lookup"><span data-stu-id="112c2-194">b.</span></span> <span data-ttu-id="112c2-195">Dans le **URL de la page connexion** champ dans Google Apps, collez la valeur hello **unique Sign-On URL du Service**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="112c2-195">In the **Sign-in page URL** field in Google Apps, paste hello value of **Single Sign-On Service URL**, which you have copied from Azure portal.</span></span>

    <span data-ttu-id="112c2-196">c.</span><span class="sxs-lookup"><span data-stu-id="112c2-196">c.</span></span> <span data-ttu-id="112c2-197">Bonjour **URL de la page de déconnexion** champ dans Google Apps, collez la valeur hello **URL de déconnexion**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="112c2-197">In hello **Sign-out page URL** field in Google Apps, paste hello value of **Sign-Out URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="112c2-198">d.</span><span class="sxs-lookup"><span data-stu-id="112c2-198">d.</span></span> <span data-ttu-id="112c2-199">Bonjour **modifier l’URL de mot de passe** champ dans Google Apps, collez la valeur hello **modifier l’URL de mot de passe**, lequel vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="112c2-199">In hello **Change password URL** field in Google Apps, paste hello value of **Change password URL**, which you have copied from Azure portal.</span></span> 

    <span data-ttu-id="112c2-200">e.</span><span class="sxs-lookup"><span data-stu-id="112c2-200">e.</span></span> <span data-ttu-id="112c2-201">Dans Google Apps, pourquoi **certificat de vérification**, télécharger le certificat hello que vous avez téléchargé à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="112c2-201">In Google Apps, for hello **Verification certificate**, upload hello certificate that you have downloaded from Azure portal.</span></span>

    <span data-ttu-id="112c2-202">f.</span><span class="sxs-lookup"><span data-stu-id="112c2-202">f.</span></span> <span data-ttu-id="112c2-203">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="112c2-203">Click **Save Changes**.</span></span>

> [!TIP]
> <span data-ttu-id="112c2-204">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="112c2-204">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="112c2-205">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="112c2-205">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="112c2-206">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="112c2-206">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
 
### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="112c2-207">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="112c2-207">Creating an Azure AD test user</span></span>
<span data-ttu-id="112c2-208">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="112c2-208">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="112c2-210">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="112c2-210">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="112c2-211">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="112c2-211">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="112c2-213">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="112c2-213">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="112c2-215">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="112c2-215">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="112c2-217">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="112c2-217">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-google-apps-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="112c2-219">a.</span><span class="sxs-lookup"><span data-stu-id="112c2-219">a.</span></span> <span data-ttu-id="112c2-220">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="112c2-220">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="112c2-221">b.</span><span class="sxs-lookup"><span data-stu-id="112c2-221">b.</span></span> <span data-ttu-id="112c2-222">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="112c2-222">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="112c2-223">c.</span><span class="sxs-lookup"><span data-stu-id="112c2-223">c.</span></span> <span data-ttu-id="112c2-224">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="112c2-224">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="112c2-225">d.</span><span class="sxs-lookup"><span data-stu-id="112c2-225">d.</span></span> <span data-ttu-id="112c2-226">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="112c2-226">Click **Create**.</span></span>
 
### <a name="creating-a-google-apps-test-user"></a><span data-ttu-id="112c2-227">Création d’un utilisateur de test Google Apps</span><span class="sxs-lookup"><span data-stu-id="112c2-227">Creating a Google Apps test user</span></span>

<span data-ttu-id="112c2-228">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Google Apps logiciel.</span><span class="sxs-lookup"><span data-stu-id="112c2-228">hello objective of this section is toocreate a user called Britta Simon in Google Apps Software.</span></span> <span data-ttu-id="112c2-229">Google Apps prend en charge l’approvisionnement automatique, qui est activé par défaut.</span><span class="sxs-lookup"><span data-stu-id="112c2-229">Google Apps supports auto provisioning, which is by default enabled.</span></span> <span data-ttu-id="112c2-230">Vous n’avez aucune opération à effectuer dans cette section.</span><span class="sxs-lookup"><span data-stu-id="112c2-230">There is no action for you in this section.</span></span> <span data-ttu-id="112c2-231">Si un utilisateur n’existe pas déjà dans Google Apps logiciel, un nouveau est créé lorsque vous essayez de tooaccess logiciel des applications de Google.</span><span class="sxs-lookup"><span data-stu-id="112c2-231">If a user doesn't already exist in Google Apps Software, a new one is created when you attempt tooaccess Google Apps Software.</span></span>

>[!NOTE] 
><span data-ttu-id="112c2-232">Si vous avez besoin de toocreate un utilisateur manuellement, contactez hello [équipe de support technique de Google](https://www.google.com/contact/).</span><span class="sxs-lookup"><span data-stu-id="112c2-232">If you need toocreate a user manually, contact hello [Google support team](https://www.google.com/contact/).</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="112c2-233">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="112c2-233">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="112c2-234">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès à des applications de tooGoogle.</span><span class="sxs-lookup"><span data-stu-id="112c2-234">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooGoogle Apps.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="112c2-236">**tooassign Britta Simon tooGoogle applications, effectuer hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="112c2-236">**tooassign Britta Simon tooGoogle Apps, perform hello following steps:**</span></span>

1. <span data-ttu-id="112c2-237">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="112c2-237">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="112c2-239">Dans la liste des applications hello, sélectionnez **Google Apps**.</span><span class="sxs-lookup"><span data-stu-id="112c2-239">In hello applications list, select **Google Apps**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-google-apps-tutorial/tutorial_googleapps_app.png) 

3. <span data-ttu-id="112c2-241">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="112c2-241">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="112c2-243">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="112c2-243">Click **Add** button.</span></span> <span data-ttu-id="112c2-244">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="112c2-244">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="112c2-246">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="112c2-246">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="112c2-247">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="112c2-247">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="112c2-248">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="112c2-248">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="112c2-249">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="112c2-249">Testing single sign-on</span></span>

<span data-ttu-id="112c2-250">Dans cette section, tootest votre seule paramètres d’authentification, ouvrez hello volet d’accès au [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), puis connectez-vous à un compte de test hello, puis cliquez sur **Google Apps** vignette Bonjour panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="112c2-250">In this section, tootest your single sign-on settings, open hello Access Panel at [https://myapps.microsoft.com](active-directory-saas-access-panel-introduction.md), then sign into hello test account, and click **Google Apps** tile in hello Access Panel.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="112c2-251">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="112c2-251">Additional resources</span></span>

* [<span data-ttu-id="112c2-252">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="112c2-252">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="112c2-253">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="112c2-253">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)
* [<span data-ttu-id="112c2-254">Configurer l’approvisionnement de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="112c2-254">Configure User Provisioning</span></span>](active-directory-saas-google-apps-provisioning-tutorial.md)

<!--Image references-->

[1]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-google-apps-tutorial/tutorial_general_203.png

[0]: ./media/active-directory-saas-google-apps-tutorial/azure-active-directory.png

[5]: ./media/active-directory-saas-google-apps-tutorial/gapps-added.png
[6]: ./media/active-directory-saas-google-apps-tutorial/config-sso.png
[7]: ./media/active-directory-saas-google-apps-tutorial/sso-gapps.png
[8]: ./media/active-directory-saas-google-apps-tutorial/sso-url.png
[9]: ./media/active-directory-saas-google-apps-tutorial/download-cert.png
[10]: ./media/active-directory-saas-google-apps-tutorial/gapps-security.png
[11]: ./media/active-directory-saas-google-apps-tutorial/security-gapps.png
[12]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-config.png
[13]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-confirm.png
[14]: ./media/active-directory-saas-google-apps-tutorial/gapps-sso-email.png
[15]: ./media/active-directory-saas-google-apps-tutorial/gapps-api.png
[16]: ./media/active-directory-saas-google-apps-tutorial/gapps-api-enabled.png
[17]: ./media/active-directory-saas-google-apps-tutorial/add-custom-domain.png
[18]: ./media/active-directory-saas-google-apps-tutorial/specify-domain.png
[19]: ./media/active-directory-saas-google-apps-tutorial/verify-domain.png
[20]: ./media/active-directory-saas-google-apps-tutorial/gapps-domains.png
[21]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-domain.png
[22]: ./media/active-directory-saas-google-apps-tutorial/gapps-add-another.png
[23]: ./media/active-directory-saas-google-apps-tutorial/apps-gapps.png
[24]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning.png
[25]: ./media/active-directory-saas-google-apps-tutorial/gapps-provisioning-auth.png
[26]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin.png
[27]: ./media/active-directory-saas-google-apps-tutorial/gapps-admin-privileges.png
[28]: ./media/active-directory-saas-google-apps-tutorial/gapps-auth.png
[29]: ./media/active-directory-saas-google-apps-tutorial/assign-users.png
[30]: ./media/active-directory-saas-google-apps-tutorial/assign-confirm.png