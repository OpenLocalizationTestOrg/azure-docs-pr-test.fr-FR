---
title: "Didacticiel : Intégration d’Azure Active Directory à Work.com | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Work.com."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 98e6739e-eb24-46bd-9dd3-20b489839076
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jeedes
ms.openlocfilehash: dcdc51c884abd78c945b649de99f942d32373cf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-workcom"></a><span data-ttu-id="043b0-103">Didacticiel : Intégration d’Azure AD à Work.com</span><span class="sxs-lookup"><span data-stu-id="043b0-103">Tutorial: Azure Active Directory integration with Work.com</span></span>

<span data-ttu-id="043b0-104">Dans ce didacticiel, vous apprendrez comment toointegrate Work.com avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="043b0-104">In this tutorial, you learn how toointegrate Work.com with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="043b0-105">Intégration de Work.com à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="043b0-105">Integrating Work.com with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="043b0-106">Vous pouvez contrôler dans Azure AD qui a accès tooWork.com</span><span class="sxs-lookup"><span data-stu-id="043b0-106">You can control in Azure AD who has access tooWork.com</span></span>
- <span data-ttu-id="043b0-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooWork.com (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="043b0-107">You can enable your users tooautomatically get signed-on tooWork.com (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="043b0-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="043b0-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="043b0-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="043b0-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="043b0-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="043b0-110">Prerequisites</span></span>

<span data-ttu-id="043b0-111">tooconfigure intégration d’Azure AD avec Work.com, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="043b0-111">tooconfigure Azure AD integration with Work.com, you need hello following items:</span></span>

- <span data-ttu-id="043b0-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="043b0-112">An Azure AD subscription</span></span>
- <span data-ttu-id="043b0-113">Un abonnement Work.com pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="043b0-113">A Work.com single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="043b0-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="043b0-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="043b0-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="043b0-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="043b0-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="043b0-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="043b0-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="043b0-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="043b0-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="043b0-118">Scenario description</span></span>
<span data-ttu-id="043b0-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="043b0-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="043b0-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="043b0-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="043b0-121">Ajouter des Work.com à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="043b0-121">Add Work.com from hello gallery</span></span>
2. <span data-ttu-id="043b0-122">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="043b0-122">Configure and test Azure AD single sign-on</span></span>

## <a name="add-workcom-from-hello-gallery"></a><span data-ttu-id="043b0-123">Ajouter des Work.com à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="043b0-123">Add Work.com from hello gallery</span></span>
<span data-ttu-id="043b0-124">intégration de hello tooconfigure de Work.com dans Azure AD, vous devez tooadd Work.com à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="043b0-124">tooconfigure hello integration of Work.com into Azure AD, you need tooadd Work.com from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="043b0-125">**tooadd Work.com à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="043b0-125">**tooadd Work.com from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="043b0-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="043b0-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="043b0-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="043b0-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="043b0-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="043b0-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="043b0-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="043b0-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="043b0-133">Dans la zone de recherche de hello, tapez **Work.com**, sélectionnez **Work.com** à partir du panneau résultats puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="043b0-133">In hello search box, type **Work.com**, select **Work.com** from results panel then click **Add** button tooadd hello application.</span></span>

    ![Ajouter à partir de la galerie](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="043b0-135">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="043b0-135">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="043b0-136">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Work.com avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="043b0-136">In this section, you configure and test Azure AD single sign-on with Work.com based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="043b0-137">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Work.com est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="043b0-137">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Work.com is tooa user in Azure AD.</span></span> <span data-ttu-id="043b0-138">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Work.com doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="043b0-138">In other words, a link relationship between an Azure AD user and hello related user in Work.com needs toobe established.</span></span>

<span data-ttu-id="043b0-139">Dans Work.com, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="043b0-139">In Work.com, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="043b0-140">tooconfigure et test Azure AD l’authentification unique avec Work.com, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="043b0-140">tooconfigure and test Azure AD single sign-on with Work.com, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="043b0-141">**[Configurer Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="043b0-141">**[Configure Azure AD Single Sign-On](#configure-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="043b0-142">**[Créer un utilisateur de test Azure AD](#create-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="043b0-142">**[Create an Azure AD test user](#create-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="043b0-143">**[Créer un utilisateur de test Work.com](#create-a-workcom-test-user)**  -toohave un équivalent de Britta Simon dans Work.com est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="043b0-143">**[Create a Work.com test user](#create-a-workcom-test-user)** - toohave a counterpart of Britta Simon in Work.com that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="043b0-144">**[Affecter l’utilisateur de test hello Azure AD](#assign-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="043b0-144">**[Assign hello Azure AD test user](#assign-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="043b0-145">**[Tester l’authentification unique sur](#test-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="043b0-145">**[Test Single Sign-On](#test-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="043b0-146">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="043b0-146">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="043b0-147">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Work.com.</span><span class="sxs-lookup"><span data-stu-id="043b0-147">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Work.com application.</span></span>

>[!NOTE]
><span data-ttu-id="043b0-148">tooconfigure l’authentification unique, vous devez encore toosetup un nom de domaine Work.com personnalisé.</span><span class="sxs-lookup"><span data-stu-id="043b0-148">tooconfigure single sign-on, you need toosetup a custom Work.com domain name yet.</span></span> <span data-ttu-id="043b0-149">Vous devez toodefine au moins un domaine nom, votre nom de domaine de test et déployez-le tooyour toute organisation.</span><span class="sxs-lookup"><span data-stu-id="043b0-149">You need toodefine at least a domain name, test your domain name, and deploy it tooyour entire organization.</span></span>

<span data-ttu-id="043b0-150">**tooconfigure Azure AD single sign-on avec Work.com, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="043b0-150">**tooconfigure Azure AD single sign-on with Work.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="043b0-151">Bonjour portail Azure, sur hello **Work.com** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="043b0-151">In hello Azure portal, on hello **Work.com** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="043b0-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="043b0-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Authentification basée sur SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_samlbase.png)

3. <span data-ttu-id="043b0-155">Sur hello **Work.com domaine et les URL** section, hello suivants :</span><span class="sxs-lookup"><span data-stu-id="043b0-155">On hello **Work.com Domain and URLs** section, perform hello following:</span></span>

    ![Section Domaine et URL Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_url.png)

    <span data-ttu-id="043b0-157">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`http://<companyname>.my.salesforce.com`</span><span class="sxs-lookup"><span data-stu-id="043b0-157">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `http://<companyname>.my.salesforce.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="043b0-158">Cette valeur n’est pas la valeur réelle.</span><span class="sxs-lookup"><span data-stu-id="043b0-158">This value is not real.</span></span> <span data-ttu-id="043b0-159">Mettre à jour de cette valeur avec hello URL de connexion réel.</span><span class="sxs-lookup"><span data-stu-id="043b0-159">Update this value with hello actual Sign-On URL.</span></span> <span data-ttu-id="043b0-160">Contact [équipe de support Client de Work.com](https://help.salesforce.com/articleView?id=000159855&type=3) tooget cette valeur.</span><span class="sxs-lookup"><span data-stu-id="043b0-160">Contact [Work.com Client support team](https://help.salesforce.com/articleView?id=000159855&type=3) tooget this value.</span></span> 

4. <span data-ttu-id="043b0-161">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="043b0-161">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Section Certificat de signature SAML](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_certificate.png) 

5. <span data-ttu-id="043b0-163">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="043b0-163">Click **Save** button.</span></span>

    ![Bouton Enregistrer](./media/active-directory-saas-work-com-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="043b0-165">Sur hello **Work.com Configuration** , cliquez sur **configurer de Work.com** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="043b0-165">On hello **Work.com Configuration** section, click **Configure Work.com** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="043b0-166">Hello de copie **URL de déconnexion, ID d’entité SAML et SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="043b0-166">Copy hello **Sign-Out URL, SAML Entity ID, and SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Section Configuration de Work.com](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_configure.png) 
7. <span data-ttu-id="043b0-168">Ouvrez une session dans tooyour client Work.com en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="043b0-168">Log in tooyour Work.com tenant as administrator.</span></span>

8. <span data-ttu-id="043b0-169">Accédez trop**le programme d’installation**.</span><span class="sxs-lookup"><span data-stu-id="043b0-169">Go too**Setup**.</span></span>
   
    <span data-ttu-id="043b0-170">![Configuration](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="043b0-170">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

9. <span data-ttu-id="043b0-171">Dans le volet de navigation gauche hello Bonjour **administrer** , cliquez sur **gestion des domaines** tooexpand hello section associée, puis cliquez sur **mon domaine** tooopen hello  **Mon domaine** page.</span><span class="sxs-lookup"><span data-stu-id="043b0-171">On hello left navigation pane, in hello **Administer** section, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
   
    <span data-ttu-id="043b0-172">![Mon domaine](./media/active-directory-saas-work-com-tutorial/ic767825.png "mon domaine")</span><span class="sxs-lookup"><span data-stu-id="043b0-172">![My Domain](./media/active-directory-saas-work-com-tutorial/ic767825.png "My Domain")</span></span>

10. <span data-ttu-id="043b0-173">tooverify votre domaine a été correctement configuré, assurez-vous qu’il s’agit de «**tooUsers de déploiement d’étape 4**» et passez en revue votre «**mes paramètres de domaine**».</span><span class="sxs-lookup"><span data-stu-id="043b0-173">tooverify that your domain has been set up correctly, make sure that it is in “**Step 4 Deployed tooUsers**” and review your “**My Domain Settings**”.</span></span>
   
    <span data-ttu-id="043b0-174">![Domaine déployé tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "tooUser de domaine déployés")</span><span class="sxs-lookup"><span data-stu-id="043b0-174">![Domain Deployed tooUser](./media/active-directory-saas-work-com-tutorial/ic784377.png "Domain Deployed tooUser")</span></span>

11. <span data-ttu-id="043b0-175">Ouvrez une session dans tooyour client Work.com.</span><span class="sxs-lookup"><span data-stu-id="043b0-175">Log in tooyour Work.com tenant.</span></span>

12. <span data-ttu-id="043b0-176">Accédez trop**le programme d’installation**.</span><span class="sxs-lookup"><span data-stu-id="043b0-176">Go too**Setup**.</span></span>
    
    <span data-ttu-id="043b0-177">![Configuration](./media/active-directory-saas-work-com-tutorial/ic794108.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="043b0-177">![Setup](./media/active-directory-saas-work-com-tutorial/ic794108.png "Setup")</span></span>

13. <span data-ttu-id="043b0-178">Développez hello **des contrôles de sécurité** menu, puis sur **paramètres d’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="043b0-178">Expand hello **Security Controls** menu, and then click **Single Sign-On Settings**.</span></span>
    
    <span data-ttu-id="043b0-179">![Paramètres d’authentification unique](./media/active-directory-saas-work-com-tutorial/ic794113.png "paramètres d’authentification unique")</span><span class="sxs-lookup"><span data-stu-id="043b0-179">![Single Sign-On Settings](./media/active-directory-saas-work-com-tutorial/ic794113.png "Single Sign-On Settings")</span></span>

14. <span data-ttu-id="043b0-180">Sur hello **paramètres d’authentification unique** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="043b0-180">On hello **Single Sign-On Settings** dialog page, perform hello following steps:</span></span>
    
    <span data-ttu-id="043b0-181">![SAML activé](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML activé")</span><span class="sxs-lookup"><span data-stu-id="043b0-181">![SAML Enabled](./media/active-directory-saas-work-com-tutorial/ic781026.png "SAML Enabled")</span></span>
    
    <span data-ttu-id="043b0-182">a.</span><span class="sxs-lookup"><span data-stu-id="043b0-182">a.</span></span> <span data-ttu-id="043b0-183">Sélectionnez **SAML Enabled**.</span><span class="sxs-lookup"><span data-stu-id="043b0-183">Select **SAML Enabled**.</span></span>
    
    <span data-ttu-id="043b0-184">b.</span><span class="sxs-lookup"><span data-stu-id="043b0-184">b.</span></span> <span data-ttu-id="043b0-185">Cliquez sur **Nouveau**.</span><span class="sxs-lookup"><span data-stu-id="043b0-185">Click **New**.</span></span>

15. <span data-ttu-id="043b0-186">Bonjour **paramètres d’authentification unique SAML** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="043b0-186">In hello **SAML Single Sign-On Settings** section, perform hello following steps:</span></span>
    
    <span data-ttu-id="043b0-187">![Configuration de l’authentification unique SAML](./media/active-directory-saas-work-com-tutorial/ic794114.png "Configuration de l’authentification unique SAML")</span><span class="sxs-lookup"><span data-stu-id="043b0-187">![SAML Single Sign-On Setting](./media/active-directory-saas-work-com-tutorial/ic794114.png "SAML Single Sign-On Setting")</span></span>
    
    <span data-ttu-id="043b0-188">a.</span><span class="sxs-lookup"><span data-stu-id="043b0-188">a.</span></span> <span data-ttu-id="043b0-189">Bonjour **nom** zone de texte, tapez un nom pour votre configuration.</span><span class="sxs-lookup"><span data-stu-id="043b0-189">In hello **Name** textbox, type a name for your configuration.</span></span>  
       
    > [!NOTE]
    > <span data-ttu-id="043b0-190">En fournissant une valeur pour **nom** permet de remplir automatiquement hello **nom de l’API** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="043b0-190">Providing a value for **Name** does automatically populate hello **API Name** textbox.</span></span>
    
    <span data-ttu-id="043b0-191">b.</span><span class="sxs-lookup"><span data-stu-id="043b0-191">b.</span></span> <span data-ttu-id="043b0-192">Dans **émetteur** zone de texte, valeur hello coller **ID d’entité SAML** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="043b0-192">In **Issuer** textbox, paste hello value of **SAML Entity ID** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="043b0-193">c.</span><span class="sxs-lookup"><span data-stu-id="043b0-193">c.</span></span> <span data-ttu-id="043b0-194">certificat de hello téléchargé tooupload à partir du portail Azure, cliquez sur **Parcourir**.</span><span class="sxs-lookup"><span data-stu-id="043b0-194">tooupload hello downloaded certificate from Azure portal, click **Browse**.</span></span>
    
    <span data-ttu-id="043b0-195">d.</span><span class="sxs-lookup"><span data-stu-id="043b0-195">d.</span></span> <span data-ttu-id="043b0-196">Bonjour **Id d’entité** zone de texte, type `https://salesforce-work.com`.</span><span class="sxs-lookup"><span data-stu-id="043b0-196">In hello **Entity Id** textbox, type `https://salesforce-work.com`.</span></span>
    
    <span data-ttu-id="043b0-197">e.</span><span class="sxs-lookup"><span data-stu-id="043b0-197">e.</span></span> <span data-ttu-id="043b0-198">En tant que **SAML Identity Type**, sélectionnez **Assertion contient hello ID de fédération à partir de l’objet utilisateur de hello**.</span><span class="sxs-lookup"><span data-stu-id="043b0-198">As **SAML Identity Type**, select **Assertion contains hello Federation ID from hello User object**.</span></span>
    
    <span data-ttu-id="043b0-199">f.</span><span class="sxs-lookup"><span data-stu-id="043b0-199">f.</span></span> <span data-ttu-id="043b0-200">En tant que **emplacement d’identité SAML**, sélectionnez **identité figure dans l’élément NameIdentifier de hello Hello Subject statement**.</span><span class="sxs-lookup"><span data-stu-id="043b0-200">As **SAML Identity Location**, select **Identity is in hello NameIdentfier element of hello Subject statement**.</span></span>
    
    <span data-ttu-id="043b0-201">g.</span><span class="sxs-lookup"><span data-stu-id="043b0-201">g.</span></span> <span data-ttu-id="043b0-202">Dans **Identity Provider Login URL** zone de texte, valeur hello coller **SAML Sign-On URL du Service unique** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="043b0-202">In **Identity Provider Login URL** textbox, paste hello value of **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>

    <span data-ttu-id="043b0-203">h.</span><span class="sxs-lookup"><span data-stu-id="043b0-203">h.</span></span> <span data-ttu-id="043b0-204">Dans **Identity Provider Logout URL** zone de texte, valeur hello coller **URL de déconnexion** dont vous avez copié à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="043b0-204">In **Identity Provider Logout URL** textbox, paste hello value of **Sign-Out URL** which you have copied from Azure portal.</span></span>
    
    <span data-ttu-id="043b0-205">i.</span><span class="sxs-lookup"><span data-stu-id="043b0-205">i.</span></span> <span data-ttu-id="043b0-206">Pour **Service Provider Initiated Request Binding**, sélectionnez **HTTP POST**.</span><span class="sxs-lookup"><span data-stu-id="043b0-206">As **Service Provider Initiated Request Binding**, select **HTTP Post**.</span></span>
    
    <span data-ttu-id="043b0-207">j.</span><span class="sxs-lookup"><span data-stu-id="043b0-207">j.</span></span> <span data-ttu-id="043b0-208">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="043b0-208">Click **Save**.</span></span>

16. <span data-ttu-id="043b0-209">Dans votre portail classique Work.com, dans le volet de navigation gauche hello, cliquez sur **gestion des domaines** tooexpand hello section associée, puis cliquez sur **mon domaine** tooopen hello **mon domaine**page.</span><span class="sxs-lookup"><span data-stu-id="043b0-209">In your Work.com classic portal, on hello left navigation pane, click **Domain Management** tooexpand hello related section, and then click **My Domain** tooopen hello **My Domain** page.</span></span> 
    
    <span data-ttu-id="043b0-210">![Mon domaine](./media/active-directory-saas-work-com-tutorial/ic794115.png "mon domaine")</span><span class="sxs-lookup"><span data-stu-id="043b0-210">![My Domain](./media/active-directory-saas-work-com-tutorial/ic794115.png "My Domain")</span></span>

17. <span data-ttu-id="043b0-211">Sur hello **mon domaine** page hello **Login Page Branding** , cliquez sur **modifier**.</span><span class="sxs-lookup"><span data-stu-id="043b0-211">On hello **My Domain** page, in hello **Login Page Branding** section, click **Edit**.</span></span>
    
    <span data-ttu-id="043b0-212">![Personnalisation de la page de connexion](./media/active-directory-saas-work-com-tutorial/ic767826.png "personnalisation de la page de connexion")</span><span class="sxs-lookup"><span data-stu-id="043b0-212">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic767826.png "Login Page Branding")</span></span>

14. <span data-ttu-id="043b0-213">Sur hello **Login Page Branding** page hello **Service d’authentification** section et le nom hello votre **SAML SSO Settings** s’affiche.</span><span class="sxs-lookup"><span data-stu-id="043b0-213">On hello **Login Page Branding** page, in hello **Authentication Service** section, hello name of your **SAML SSO Settings** is displayed.</span></span> <span data-ttu-id="043b0-214">Sélectionnez-le, puis cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="043b0-214">Select it, and then click **Save**.</span></span>
    
    <span data-ttu-id="043b0-215">![Personnalisation de la page de connexion](./media/active-directory-saas-work-com-tutorial/ic784366.png "personnalisation de la page de connexion")</span><span class="sxs-lookup"><span data-stu-id="043b0-215">![Login Page Branding](./media/active-directory-saas-work-com-tutorial/ic784366.png "Login Page Branding")</span></span>

> [!TIP]
> <span data-ttu-id="043b0-216">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="043b0-216">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="043b0-217">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="043b0-217">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="043b0-218">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="043b0-218">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="043b0-219">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="043b0-219">Create an Azure AD test user</span></span>
<span data-ttu-id="043b0-220">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="043b0-220">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="043b0-222">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="043b0-222">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="043b0-223">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="043b0-223">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-work-com-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="043b0-225">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="043b0-225">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Utilisateurs et groupes -> Tous les utilisateurs](./media/active-directory-saas-work-com-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="043b0-227">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="043b0-227">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Ajouter](./media/active-directory-saas-work-com-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="043b0-229">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="043b0-229">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Boîte de dialogue utilisateur](./media/active-directory-saas-work-com-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="043b0-231">a.</span><span class="sxs-lookup"><span data-stu-id="043b0-231">a.</span></span> <span data-ttu-id="043b0-232">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="043b0-232">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="043b0-233">b.</span><span class="sxs-lookup"><span data-stu-id="043b0-233">b.</span></span> <span data-ttu-id="043b0-234">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="043b0-234">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="043b0-235">c.</span><span class="sxs-lookup"><span data-stu-id="043b0-235">c.</span></span> <span data-ttu-id="043b0-236">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="043b0-236">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="043b0-237">d.</span><span class="sxs-lookup"><span data-stu-id="043b0-237">d.</span></span> <span data-ttu-id="043b0-238">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="043b0-238">Click **Create**.</span></span>
 
### <a name="create-a-workcom-test-user"></a><span data-ttu-id="043b0-239">Créer un utilisateur de test Work.com</span><span class="sxs-lookup"><span data-stu-id="043b0-239">Create a Work.com test user</span></span>
<span data-ttu-id="043b0-240">Pour Azure Active Directory utilisateurs toobe en mesure de toosign dans, ils doivent être mis en service tooWork.com. Dans les cas de hello de Work.com, cette configuration est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="043b0-240">For Azure Active Directory users toobe able toosign in, they must be provisioned tooWork.com. In hello case of Work.com, provisioning is a manual task.</span></span>

### <a name="tooconfigure-user-provisioning-perform-hello-following-steps"></a><span data-ttu-id="043b0-241">configuration, de l’utilisateur tooconfigure effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="043b0-241">tooconfigure user provisioning, perform hello following steps:</span></span>
1. <span data-ttu-id="043b0-242">Se connecter tooyour site d’entreprise Work.com en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="043b0-242">Sign on tooyour Work.com company site as an administrator.</span></span>

2. <span data-ttu-id="043b0-243">Accédez trop**le programme d’installation**.</span><span class="sxs-lookup"><span data-stu-id="043b0-243">Go too**Setup**.</span></span>
   
    <span data-ttu-id="043b0-244">![Configuration](./media/active-directory-saas-work-com-tutorial/IC794108.png "Configuration")</span><span class="sxs-lookup"><span data-stu-id="043b0-244">![Setup](./media/active-directory-saas-work-com-tutorial/IC794108.png "Setup")</span></span>
3. <span data-ttu-id="043b0-245">Accédez trop**gérer les utilisateurs \> utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="043b0-245">Go too**Manage Users \> Users**.</span></span>
   
    <span data-ttu-id="043b0-246">![Gestion des utilisateurs](./media/active-directory-saas-work-com-tutorial/IC784369.png "Gestion des utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="043b0-246">![Manage Users](./media/active-directory-saas-work-com-tutorial/IC784369.png "Manage Users")</span></span>

4. <span data-ttu-id="043b0-247">Cliquez sur **New User**.</span><span class="sxs-lookup"><span data-stu-id="043b0-247">Click **New User**.</span></span>
   
    <span data-ttu-id="043b0-248">![Tous les utilisateurs](./media/active-directory-saas-work-com-tutorial/IC794117.png "Tous les utilisateurs")</span><span class="sxs-lookup"><span data-stu-id="043b0-248">![All Users](./media/active-directory-saas-work-com-tutorial/IC794117.png "All Users")</span></span>

5. <span data-ttu-id="043b0-249">Bonjour section modification utilisateur, effectuer hello comme suit, dans les attributs d’un Azure valide compte AD tooprovision dans hello relatives des zones de texte :</span><span class="sxs-lookup"><span data-stu-id="043b0-249">In hello User Edit section, perform hello following steps, in attributes of a valid Azure AD account you want tooprovision into hello related textboxes:</span></span>
   
    <span data-ttu-id="043b0-250">![Modification de l’utilisateur](./media/active-directory-saas-work-com-tutorial/ic794118.png "modification de l’utilisateur")</span><span class="sxs-lookup"><span data-stu-id="043b0-250">![User Edit](./media/active-directory-saas-work-com-tutorial/ic794118.png "User Edit")</span></span>
   
    <span data-ttu-id="043b0-251">a.</span><span class="sxs-lookup"><span data-stu-id="043b0-251">a.</span></span> <span data-ttu-id="043b0-252">Bonjour **prénom** hello de type zone de texte **prénom** d’utilisateur de hello **Brian**.</span><span class="sxs-lookup"><span data-stu-id="043b0-252">In hello **First Name** textbox, type hello **first name** of hello user **Britta**.</span></span>
    
    <span data-ttu-id="043b0-253">b.</span><span class="sxs-lookup"><span data-stu-id="043b0-253">b.</span></span> <span data-ttu-id="043b0-254">Bonjour **nom** hello de type zone de texte **nom** d’utilisateur de hello **Simon**.</span><span class="sxs-lookup"><span data-stu-id="043b0-254">In hello **Last Name** textbox, type hello **last name** of hello user **Simon**.</span></span>
    
    <span data-ttu-id="043b0-255">c.</span><span class="sxs-lookup"><span data-stu-id="043b0-255">c.</span></span> <span data-ttu-id="043b0-256">Bonjour **Alias** hello de type zone de texte **nom** d’utilisateur de hello **BrittaS**.</span><span class="sxs-lookup"><span data-stu-id="043b0-256">In hello **Alias** textbox, type hello **name** of hello user **BrittaS**.</span></span>
    
    <span data-ttu-id="043b0-257">d.</span><span class="sxs-lookup"><span data-stu-id="043b0-257">d.</span></span> <span data-ttu-id="043b0-258">Bonjour **messagerie** hello de type zone de texte **adresse de messagerie** d’utilisateur  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="043b0-258">In hello **Email** textbox, type hello **email address** of user **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="043b0-259">e.</span><span class="sxs-lookup"><span data-stu-id="043b0-259">e.</span></span> <span data-ttu-id="043b0-260">Bonjour **nom d’utilisateur** zone de texte, tapez un nom d’utilisateur de l’utilisateur comme  **Brittasimon@contoso.com** .</span><span class="sxs-lookup"><span data-stu-id="043b0-260">In hello **User Name** textbox, type a user name of user like **Brittasimon@contoso.com**.</span></span>
    
    <span data-ttu-id="043b0-261">f.</span><span class="sxs-lookup"><span data-stu-id="043b0-261">f.</span></span> <span data-ttu-id="043b0-262">Bonjour **surnom** zone de texte, tapez un **surnom** d’utilisateur **Simon**.</span><span class="sxs-lookup"><span data-stu-id="043b0-262">In hello **Nick Name** textbox, type a **nick name** of user **Simon**.</span></span>
    
    <span data-ttu-id="043b0-263">g.</span><span class="sxs-lookup"><span data-stu-id="043b0-263">g.</span></span> <span data-ttu-id="043b0-264">Sélectionnez **Rôle**, **Licence utilisateur** et **Profil**.</span><span class="sxs-lookup"><span data-stu-id="043b0-264">Select **Role**, **User License**, and **Profile**.</span></span>
    
    <span data-ttu-id="043b0-265">h.</span><span class="sxs-lookup"><span data-stu-id="043b0-265">h.</span></span> <span data-ttu-id="043b0-266">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="043b0-266">Click **Save**.</span></span>  
      
    > [!NOTE]
    > <span data-ttu-id="043b0-267">détenteur du compte de Hello Azure AD reçoit un message électronique contenant un compte de hello tooconfirm lien avant son activation.</span><span class="sxs-lookup"><span data-stu-id="043b0-267">hello Azure AD account holder will get an email including a link tooconfirm hello account before it becomes active.</span></span>
    > 
    > 

### <a name="assign-hello-azure-ad-test-user"></a><span data-ttu-id="043b0-268">Affecter l’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="043b0-268">Assign hello Azure AD test user</span></span>

<span data-ttu-id="043b0-269">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooWork.com.</span><span class="sxs-lookup"><span data-stu-id="043b0-269">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooWork.com.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="043b0-271">**tooassign Britta Simon tooWork.com, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="043b0-271">**tooassign Britta Simon tooWork.com, perform hello following steps:**</span></span>

1. <span data-ttu-id="043b0-272">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="043b0-272">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="043b0-274">Dans la liste des applications hello, sélectionnez **Work.com**.</span><span class="sxs-lookup"><span data-stu-id="043b0-274">In hello applications list, select **Work.com**.</span></span>

    ![Work.com dans la liste des applications](./media/active-directory-saas-work-com-tutorial/tutorial_work-com_app.png) 

3. <span data-ttu-id="043b0-276">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="043b0-276">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="043b0-278">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="043b0-278">Click **Add** button.</span></span> <span data-ttu-id="043b0-279">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="043b0-279">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="043b0-281">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="043b0-281">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="043b0-282">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="043b0-282">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="043b0-283">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="043b0-283">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="043b0-284">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="043b0-284">Test single sign-on</span></span>

<span data-ttu-id="043b0-285">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="043b0-285">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="043b0-286">Lorsque vous cliquez sur mosaïque Work.com hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Work.com application.</span><span class="sxs-lookup"><span data-stu-id="043b0-286">When you click hello Work.com tile in hello Access Panel, you should get automatically signed-on tooyour Work.com application.</span></span>
<span data-ttu-id="043b0-287">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="043b0-287">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="043b0-288">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="043b0-288">Additional resources</span></span>

* [<span data-ttu-id="043b0-289">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="043b0-289">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="043b0-290">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="043b0-290">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-work-com-tutorial/tutorial_general_203.png

