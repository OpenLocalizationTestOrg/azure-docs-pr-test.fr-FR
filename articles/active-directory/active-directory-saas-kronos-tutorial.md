---
title: "Didacticiel : Intégration d’Azure Active Directory à Kronos | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Kronos."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: e28d6191-c375-43c6-b2df-22daa88d9939
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jeedes
ms.openlocfilehash: 16fd5c203162d10b78f51b00d79017adaf8632c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-kronos"></a><span data-ttu-id="79558-103">Didacticiel : Intégration d’Azure Active Directory à Kronos</span><span class="sxs-lookup"><span data-stu-id="79558-103">Tutorial: Azure Active Directory integration with Kronos</span></span>

<span data-ttu-id="79558-104">Dans ce didacticiel, vous apprendrez comment toointegrate Kronos avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="79558-104">In this tutorial, you learn how toointegrate Kronos with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="79558-105">Intégration Kronos à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="79558-105">Integrating Kronos with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="79558-106">Vous pouvez contrôler dans Azure AD qui a accès tooKronos</span><span class="sxs-lookup"><span data-stu-id="79558-106">You can control in Azure AD who has access tooKronos</span></span>
- <span data-ttu-id="79558-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooKronos (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="79558-107">You can enable your users tooautomatically get signed-on tooKronos (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="79558-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="79558-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="79558-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="79558-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79558-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="79558-110">Prerequisites</span></span>

<span data-ttu-id="79558-111">tooconfigure intégration d’Azure AD avec Kronos, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="79558-111">tooconfigure Azure AD integration with Kronos, you need hello following items:</span></span>

- <span data-ttu-id="79558-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="79558-112">An Azure AD subscription</span></span>
- <span data-ttu-id="79558-113">Un abonnement **Kronos Workforce Central** pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="79558-113">A **Kronos Workforce Central** SSO enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="79558-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="79558-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="79558-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="79558-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="79558-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="79558-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="79558-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="79558-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="79558-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="79558-118">Scenario description</span></span>
<span data-ttu-id="79558-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="79558-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="79558-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="79558-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="79558-121">Ajout de Kronos à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="79558-121">Adding Kronos from hello gallery</span></span>
2. <span data-ttu-id="79558-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="79558-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-kronos-from-hello-gallery"></a><span data-ttu-id="79558-123">Ajout de Kronos à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="79558-123">Adding Kronos from hello gallery</span></span>
<span data-ttu-id="79558-124">tooconfigure hello intégration de Kronos dans Azure AD, vous devez tooadd Kronos à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="79558-124">tooconfigure hello integration of Kronos into Azure AD, you need tooadd Kronos from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="79558-125">**tooadd Kronos à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="79558-125">**tooadd Kronos from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="79558-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="79558-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="79558-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="79558-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="79558-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="79558-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="79558-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="79558-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="79558-133">Dans la zone de recherche de hello, tapez **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="79558-133">In hello search box, type **Kronos**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_search.png)

5. <span data-ttu-id="79558-135">Dans le volet de résultats hello, sélectionnez **Kronos**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="79558-135">In hello results panel, select **Kronos**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="79558-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="79558-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="79558-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Kronos avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="79558-138">In this section, you configure and test Azure AD single sign-on with Kronos based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="79558-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Kronos est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79558-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Kronos is tooa user in Azure AD.</span></span> <span data-ttu-id="79558-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Kronos doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="79558-140">In other words, a link relationship between an Azure AD user and hello related user in Kronos needs toobe established.</span></span>

<span data-ttu-id="79558-141">Dans Kronos, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="79558-141">In Kronos, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="79558-142">tooconfigure et test Azure AD l’authentification unique avec Kronos, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="79558-142">tooconfigure and test Azure AD single sign-on with Kronos, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="79558-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="79558-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="79558-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="79558-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="79558-145">**[Création d’un utilisateur de test Kronos](#creating-a-kronos-test-user)**  -toohave un équivalent de Britta Simon dans Kronos est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="79558-145">**[Creating a Kronos test user](#creating-a-kronos-test-user)** - toohave a counterpart of Britta Simon in Kronos that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="79558-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="79558-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="79558-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="79558-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="79558-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="79558-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="79558-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Kronos.</span><span class="sxs-lookup"><span data-stu-id="79558-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Kronos application.</span></span>

<span data-ttu-id="79558-150">**tooconfigure Azure AD single sign-on avec Kronos, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="79558-150">**tooconfigure Azure AD single sign-on with Kronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="79558-151">Bonjour portail Azure, sur hello **Kronos** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="79558-151">In hello Azure portal, on hello **Kronos** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="79558-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="79558-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_samlbase.png)

3. <span data-ttu-id="79558-155">Sur hello **Kronos domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="79558-155">On hello **Kronos Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_url.png)

    <span data-ttu-id="79558-157">a.</span><span class="sxs-lookup"><span data-stu-id="79558-157">a.</span></span> <span data-ttu-id="79558-158">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.kronos.net/`</span><span class="sxs-lookup"><span data-stu-id="79558-158">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/`</span></span>

    <span data-ttu-id="79558-159">b.</span><span class="sxs-lookup"><span data-stu-id="79558-159">b.</span></span> <span data-ttu-id="79558-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span><span class="sxs-lookup"><span data-stu-id="79558-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<company name>.kronos.net/wfc/navigator/logonWithUID`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="79558-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="79558-161">These values are not real.</span></span> <span data-ttu-id="79558-162">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="79558-162">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="79558-163">Contact [équipe de support technique Kronos](https://www.kronos.in/contact/en-in/form) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="79558-163">Contact [Kronos support team](https://www.kronos.in/contact/en-in/form) tooget these values.</span></span>
 
4. <span data-ttu-id="79558-164">Votre application Kronos attend les assertions SAML hello dans un format spécifique.</span><span class="sxs-lookup"><span data-stu-id="79558-164">Your Kronos application expects hello SAML assertions in a specific format.</span></span> <span data-ttu-id="79558-165">Travailler avec [équipe de support technique Kronos](https://www.kronos.in/contact/en-in/form) première tooidentify hello correct identifiant d’utilisateur, qui est mappée à une application hello.</span><span class="sxs-lookup"><span data-stu-id="79558-165">Work with [Kronos support team](https://www.kronos.in/contact/en-in/form) first tooidentify hello correct user identifier, which is mapped into hello application.</span></span> <span data-ttu-id="79558-166">Prenez également les conseils hello d’attribut hello, qui souhaite toouse pour ce mappage.</span><span class="sxs-lookup"><span data-stu-id="79558-166">Also please take hello guidance about hello attribute, which they want toouse for this mapping.</span></span>
 
     <span data-ttu-id="79558-167">Microsoft recommande d’utiliser hello **« NameIdentifier »** attribut sous la forme d’identificateur de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="79558-167">Microsoft recommends using hello **"NameIdentifier"** attribute as user identifier.</span></span> <span data-ttu-id="79558-168">Vous pouvez gérer les valeurs de ces attributs hello depuis hello **« Attributs utilisateur »** section sur la page d’intégration d’application.</span><span class="sxs-lookup"><span data-stu-id="79558-168">You can manage hello values of these attributes from hello **"User Attributes"** section on application integration page.</span></span>
     
     <span data-ttu-id="79558-169">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="79558-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="79558-170">Ici, nous avons mappé hello **identificateur d’utilisateur (nameid)** avec **ExtractMailPrefix()** fonction de **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="79558-170">Here we have mapped hello **User Identifier (nameid)** with **ExtractMailPrefix()** function of **user.userprincipalname**.</span></span> <span data-ttu-id="79558-171">Cela donne la valeur hello préfixe par courrier électronique des utilisateur hello qui est hello ID utilisateur unique.</span><span class="sxs-lookup"><span data-stu-id="79558-171">This gives hello prefix value of email of hello user which is hello unique User ID.</span></span> <span data-ttu-id="79558-172">Ceci est envoyé toohello Kronos application chaque réponse correcte.</span><span class="sxs-lookup"><span data-stu-id="79558-172">This is sent toohello Kronos application in every successful response.</span></span> 
     
    ![Configurer l’authentification unique](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_attribute.png)

5. <span data-ttu-id="79558-174">Bonjour **attributs utilisateur** section hello **l’authentification unique** boîte de dialogue :</span><span class="sxs-lookup"><span data-stu-id="79558-174">In hello **User Attributes** section on hello **Single sign-on** dialog:</span></span>

    <span data-ttu-id="79558-175">a.</span><span class="sxs-lookup"><span data-stu-id="79558-175">a.</span></span> <span data-ttu-id="79558-176">Dans la liste de déroulante hello identificateur d’utilisateur, sélectionnez **ExtractMailPrefix**.</span><span class="sxs-lookup"><span data-stu-id="79558-176">In hello User Identifier dropdown list, select **ExtractMailPrefix**.</span></span>

    <span data-ttu-id="79558-177">b.</span><span class="sxs-lookup"><span data-stu-id="79558-177">b.</span></span> <span data-ttu-id="79558-178">Bonjour **Mail** liste déroulante, sélectionnez **user.userprincipalname**.</span><span class="sxs-lookup"><span data-stu-id="79558-178">In hello **Mail** dropdown list, select **user.userprincipalname**.</span></span>

6. <span data-ttu-id="79558-179">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="79558-179">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_certificate.png) 

7. <span data-ttu-id="79558-181">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="79558-181">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kronos-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="79558-183">tooconfigure l’authentification unique sur **Kronos** côté, vous devez hello toosend téléchargé **Metadata XML** trop[équipe de support technique Kronos](https://www.kronos.in/contact/en-in/form).</span><span class="sxs-lookup"><span data-stu-id="79558-183">tooconfigure single sign-on on **Kronos** side, you need toosend hello downloaded **Metadata XML** too[Kronos support team](https://www.kronos.in/contact/en-in/form).</span></span> 

> [!TIP]
> <span data-ttu-id="79558-184">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="79558-184">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="79558-185">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="79558-185">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="79558-186">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="79558-186">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="79558-187">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="79558-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="79558-188">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="79558-188">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="79558-190">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="79558-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="79558-191">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="79558-191">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="79558-193">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="79558-193">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="79558-195">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="79558-195">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="79558-197">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="79558-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kronos-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="79558-199">a.</span><span class="sxs-lookup"><span data-stu-id="79558-199">a.</span></span> <span data-ttu-id="79558-200">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="79558-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="79558-201">b.</span><span class="sxs-lookup"><span data-stu-id="79558-201">b.</span></span> <span data-ttu-id="79558-202">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="79558-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="79558-203">c.</span><span class="sxs-lookup"><span data-stu-id="79558-203">c.</span></span> <span data-ttu-id="79558-204">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="79558-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="79558-205">d.</span><span class="sxs-lookup"><span data-stu-id="79558-205">d.</span></span> <span data-ttu-id="79558-206">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="79558-206">Click **Create**.</span></span>
 
### <a name="creating-a-kronos-test-user"></a><span data-ttu-id="79558-207">Création d’un utilisateur de test Kronos</span><span class="sxs-lookup"><span data-stu-id="79558-207">Creating a Kronos test user</span></span>

<span data-ttu-id="79558-208">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Kronos.</span><span class="sxs-lookup"><span data-stu-id="79558-208">In this section, you create a user called Britta Simon in Kronos.</span></span> <span data-ttu-id="79558-209">Kronos application a besoin de toutes les toobe d’utilisateurs hello configuré dans l’application hello avant de procéder à l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="79558-209">Kronos application needs all hello users toobe provisioned in hello application before doing SSO.</span></span> 

<span data-ttu-id="79558-210">Travailler avec hello [équipe de support technique Kronos](https://www.kronos.in/contact/en-in/form) tooprovision tous ces utilisateurs dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="79558-210">Work with hello [Kronos support team](https://www.kronos.in/contact/en-in/form) tooprovision all these users into hello application.</span></span> 

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="79558-211">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="79558-211">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="79558-212">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooKronos.</span><span class="sxs-lookup"><span data-stu-id="79558-212">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooKronos.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="79558-214">**tooassign Britta Simon tooKronos, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="79558-214">**tooassign Britta Simon tooKronos, perform hello following steps:**</span></span>

1. <span data-ttu-id="79558-215">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="79558-215">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="79558-217">Dans la liste des applications hello, sélectionnez **Kronos**.</span><span class="sxs-lookup"><span data-stu-id="79558-217">In hello applications list, select **Kronos**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-kronos-tutorial/tutorial_kronos_app.png) 

3. <span data-ttu-id="79558-219">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="79558-219">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="79558-221">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="79558-221">Click **Add** button.</span></span> <span data-ttu-id="79558-222">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="79558-222">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="79558-224">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="79558-224">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="79558-225">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="79558-225">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="79558-226">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="79558-226">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="79558-227">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="79558-227">Testing single sign-on</span></span>

<span data-ttu-id="79558-228">Dans cette section, vous tester votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="79558-228">In this section, you test your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="79558-229">Lorsque vous cliquez sur hello Kronos vignette Bonjour volet d’accès, vous devez obtenir automatiquement signé sur tooyour Kronos application.</span><span class="sxs-lookup"><span data-stu-id="79558-229">When you click hello Kronos tile in hello Access Panel, you should get automatically signed-on tooyour Kronos application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="79558-230">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="79558-230">Additional resources</span></span>

* [<span data-ttu-id="79558-231">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="79558-231">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="79558-232">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="79558-232">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kronos-tutorial/tutorial_general_203.png

