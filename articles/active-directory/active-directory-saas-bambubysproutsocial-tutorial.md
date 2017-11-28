---
title: "Didacticiel : Intégration d’Azure Active Directory à Bambu by Sprout Social | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Bambu par pousses sociaux."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: d2b9ddbc-cab7-40d6-aca1-5b171cab4199
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: jeedes
ms.openlocfilehash: c9998772c032476f9a18054873022f55b4bb78be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-bambu-by-sprout-social"></a><span data-ttu-id="50086-103">Didacticiel : Intégration d’Azure Active Directory à Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="50086-103">Tutorial: Azure Active Directory integration with Bambu by Sprout Social</span></span>

<span data-ttu-id="50086-104">Dans ce didacticiel, vous apprendrez comment toointegrate Bambu par pousses sociaux avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="50086-104">In this tutorial, you learn how toointegrate Bambu by Sprout Social with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="50086-105">Intégration Bambu par pousses Social à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="50086-105">Integrating Bambu by Sprout Social with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="50086-106">Vous pouvez contrôler dans Azure AD qui a tooBambu d’accès par pousses Social</span><span class="sxs-lookup"><span data-stu-id="50086-106">You can control in Azure AD who has access tooBambu by Sprout Social</span></span>
- <span data-ttu-id="50086-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooBambu par pousses sociaux (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="50086-107">You can enable your users tooautomatically get signed-on tooBambu by Sprout Social (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="50086-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="50086-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="50086-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="50086-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

<!--## Overview

tooenable single sign-on with Bambu by Sprout Social, it must be configured toouse Azure Active Directory as an identity provider. This guide provides information and tips on how tooperform this configuration in Bambu by Sprout Social.

>[!Note]: 
>This embedded guide is brand new in hello new Azure portal, and we’d love toohear your thoughts. Use hello Feedback ? button at hello top of hello portal tooprovide feedback. hello older guide for using hello [Azure classic portal](https://manage.windowsazure.com) tooconfigure this application can be found [here](https://github.com/Azure/AzureAD-App-Docs/blob/master/articles/en-us/_/sso_configure.md).-->


## <a name="prerequisites"></a><span data-ttu-id="50086-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="50086-110">Prerequisites</span></span>

<span data-ttu-id="50086-111">tooconfigure intégration d’Azure AD avec Bambu par pousses sociaux, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="50086-111">tooconfigure Azure AD integration with Bambu by Sprout Social, you need hello following items:</span></span>

- <span data-ttu-id="50086-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="50086-112">An Azure AD subscription</span></span>
- <span data-ttu-id="50086-113">Un abonnement Bambu by Sprout Social pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="50086-113">A Bambu by Sprout Social single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="50086-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="50086-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="50086-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="50086-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="50086-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="50086-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="50086-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="50086-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="50086-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="50086-118">Scenario description</span></span>
<span data-ttu-id="50086-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="50086-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="50086-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="50086-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="50086-121">Ajout de Bambu par pousses Social à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="50086-121">Adding Bambu by Sprout Social from hello gallery</span></span>
2. <span data-ttu-id="50086-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="50086-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-bambu-by-sprout-social-from-hello-gallery"></a><span data-ttu-id="50086-123">Ajout de Bambu par pousses Social à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="50086-123">Adding Bambu by Sprout Social from hello gallery</span></span>
<span data-ttu-id="50086-124">intégration de hello tooconfigure de Bambu par pousses sociaux dans Azure AD, vous devez tooadd Bambu par pousses Social à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="50086-124">tooconfigure hello integration of Bambu by Sprout Social into Azure AD, you need tooadd Bambu by Sprout Social from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="50086-125">**tooadd Bambu par pousses Social à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="50086-125">**tooadd Bambu by Sprout Social from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="50086-126">Bonjour  **[Azure Portal](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="50086-126">In hello **[Azure Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="50086-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="50086-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="50086-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="50086-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="50086-131">Cliquez sur **nouvelle application** bouton en haut de hello de nouvelle application hello dialogue tooadd.</span><span class="sxs-lookup"><span data-stu-id="50086-131">Click **New application** button on hello top of hello dialog tooadd new application.</span></span>

    ![Applications][3]

4. <span data-ttu-id="50086-133">Dans la zone de recherche de hello, tapez **Bambu par pousses sociaux**.</span><span class="sxs-lookup"><span data-stu-id="50086-133">In hello search box, type **Bambu by Sprout Social**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_search.png)

5. <span data-ttu-id="50086-135">Dans le volet de résultats hello, sélectionnez **Bambu par pousses sociaux**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="50086-135">In hello results panel, select **Bambu by Sprout Social**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="50086-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="50086-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="50086-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Bambu by Sprout Social sur un utilisateur de test nommé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="50086-138">In this section, you configure and test Azure AD single sign-on with Bambu by Sprout Social based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="50086-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Bambu par pousses Social est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="50086-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Bambu by Sprout Social is tooa user in Azure AD.</span></span> <span data-ttu-id="50086-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Bambu par pousses sociaux doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="50086-140">In other words, a link relationship between an Azure AD user and hello related user in Bambu by Sprout Social needs toobe established.</span></span>

<span data-ttu-id="50086-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Bambu par pousses sociaux.</span><span class="sxs-lookup"><span data-stu-id="50086-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Bambu by Sprout Social.</span></span>

<span data-ttu-id="50086-142">tooconfigure et test Azure AD l’authentification unique avec Bambu par pousses sociaux, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="50086-142">tooconfigure and test Azure AD single sign-on with Bambu by Sprout Social, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="50086-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="50086-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="50086-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="50086-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="50086-145">**[Création d’un Bambu par l’utilisateur de test pousses sociaux](#creating-a-bambu-by-sprout-social-test-user)**  -toohave de Britta Simon dans Bambu par pousses Social qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="50086-145">**[Creating a Bambu by Sprout Social test user](#creating-a-bambu-by-sprout-social-test-user)** - toohave a counterpart of Britta Simon in Bambu by Sprout Social that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="50086-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="50086-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="50086-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="50086-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="50086-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="50086-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="50086-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre Bambu par application pousses sociaux.</span><span class="sxs-lookup"><span data-stu-id="50086-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Bambu by Sprout Social application.</span></span>

<span data-ttu-id="50086-150">**tooconfigure Azure AD l’authentification unique avec Bambu par pousses sociaux, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="50086-150">**tooconfigure Azure AD single sign-on with Bambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="50086-151">Bonjour portail Azure, sur hello **Bambu par pousses sociaux** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="50086-151">In hello Azure portal, on hello **Bambu by Sprout Social** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="50086-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="50086-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_samlbase.png)

3. <span data-ttu-id="50086-155">Sur hello **Bambu par URL et de domaine de réseaux sociaux pousses** section, hello utilisateur n’est pas tooperform toutes les étapes que l’application hello est déjà pré-intégration à Azure.</span><span class="sxs-lookup"><span data-stu-id="50086-155">On hello **Bambu by Sprout Social Domain and URLs** section, hello user does not have tooperform any steps as hello app is already pre-integrated with Azure.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_url.png)

4. <span data-ttu-id="50086-157">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="50086-157">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_certificate.png) 

5. <span data-ttu-id="50086-159">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="50086-159">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_400.png)
    
6. <span data-ttu-id="50086-161">Sur hello **Bambu par la Configuration de réseaux sociaux pousses** , cliquez sur **Bambu de configurer par pousses sociaux** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="50086-161">On hello **Bambu by Sprout Social Configuration** section, click **Configure Bambu by Sprout Social** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="50086-162">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="50086-162">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_configure.png) 

7. <span data-ttu-id="50086-164">tooconfigure l’authentification unique sur **Bambu par pousses sociaux** côté, vous devez hello toosend téléchargé **Metadata XML** et **SAML Sign-On URL du Service unique** trop[Bambu par le support technique de pousses sociaux](mailto:support@getbambu.com).</span><span class="sxs-lookup"><span data-stu-id="50086-164">tooconfigure single sign-on on **Bambu by Sprout Social** side, you need toosend hello downloaded **Metadata XML** and **SAML Single Sign-On Service URL** too[Bambu by Sprout Social support](mailto:support@getbambu.com).</span></span> <span data-ttu-id="50086-165">Ils seront configurer Bonjour de toohave commande connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="50086-165">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="50086-166">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="50086-166">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="50086-167">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** section, cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="50086-167">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click on hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="50086-168">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="50086-168">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

<!--### Next steps

tooensure users can sign-in tooBambu by Sprout Social after it has been configured toouse Azure Active Directory, review hello following tasks and topics:

- User accounts must be pre-provisioned into Bambu by Sprout Social prior toosign-in. tooset this up, see Provisioning.
 
- Users must be assigned access tooBambu by Sprout Social in Azure AD toosign-in. tooassign users, see Users.
 
- tooconfigure access polices for Bambu by Sprout Social users, see Access Policies.
 
- For additional information on deploying single sign-on toousers, see [this article](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users).-->


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="50086-169">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="50086-169">Creating an Azure AD test user</span></span>
<span data-ttu-id="50086-170">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="50086-170">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="50086-172">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="50086-172">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="50086-173">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="50086-173">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="50086-175">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="50086-175">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="50086-177">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="50086-177">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="50086-179">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="50086-179">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-bambubysproutsocial-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="50086-181">a.</span><span class="sxs-lookup"><span data-stu-id="50086-181">a.</span></span> <span data-ttu-id="50086-182">Bonjour **nom** zone de texte, type **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="50086-182">In hello **Name** textbox, type **Britta Simon**.</span></span>

    <span data-ttu-id="50086-183">b.</span><span class="sxs-lookup"><span data-stu-id="50086-183">b.</span></span> <span data-ttu-id="50086-184">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="50086-184">In hello **User name** textbox, type hello **email address** of Britta Simon.</span></span>

    <span data-ttu-id="50086-185">c.</span><span class="sxs-lookup"><span data-stu-id="50086-185">c.</span></span> <span data-ttu-id="50086-186">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="50086-186">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="50086-187">d.</span><span class="sxs-lookup"><span data-stu-id="50086-187">d.</span></span> <span data-ttu-id="50086-188">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="50086-188">Click **Create**.</span></span>
 
### <a name="creating-a-bambu-by-sprout-social-test-user"></a><span data-ttu-id="50086-189">Création d’un utilisateur de test Bambu by Sprout Social</span><span class="sxs-lookup"><span data-stu-id="50086-189">Creating a Bambu by Sprout Social test user</span></span>

<span data-ttu-id="50086-190">Application prend en charge juste configuration en temps utilisateur et une fois que les utilisateurs de l’authentification seront créées automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="50086-190">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="50086-191">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="50086-191">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="50086-192">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooBambu d’accès par pousses sociaux.</span><span class="sxs-lookup"><span data-stu-id="50086-192">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooBambu by Sprout Social.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="50086-194">**tooassign tooBambu Britta Simon par pousses sociaux, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="50086-194">**tooassign Britta Simon tooBambu by Sprout Social, perform hello following steps:**</span></span>

1. <span data-ttu-id="50086-195">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="50086-195">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="50086-197">Dans la liste des applications hello, sélectionnez **Bambu par pousses sociaux**.</span><span class="sxs-lookup"><span data-stu-id="50086-197">In hello applications list, select **Bambu by Sprout Social**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_bambubysproutsocial_app.png) 

3. <span data-ttu-id="50086-199">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="50086-199">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="50086-201">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="50086-201">Click **Add** button.</span></span> <span data-ttu-id="50086-202">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="50086-202">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="50086-204">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="50086-204">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="50086-205">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="50086-205">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="50086-206">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="50086-206">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="50086-207">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="50086-207">Testing single sign-on</span></span>

<span data-ttu-id="50086-208">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="50086-208">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="50086-209">Lorsque vous cliquez sur hello Bambu par vignette pousses sociaux Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Bambu par application pousses sociaux.</span><span class="sxs-lookup"><span data-stu-id="50086-209">When you click hello Bambu by Sprout Social tile in hello Access Panel, you should get automatically signed-on tooyour Bambu by Sprout Social application.</span></span> <span data-ttu-id="50086-210">Pour plus d'informations sur le panneau d'accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="50086-210">For more details about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="50086-211">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="50086-211">Additional resources</span></span>

* [<span data-ttu-id="50086-212">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50086-212">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="50086-213">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="50086-213">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-bambubysproutsocial-tutorial/tutorial_general_203.png

