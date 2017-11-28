---
title: "Didacticiel : Intégration d’Azure Active Directory à Ariba | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Ariba."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 45a8364c-55d1-4dc7-b079-9eb2a701842d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: jeedes
ms.openlocfilehash: a1b17129c1298b59c155a0890e41e41ff9544a24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ariba"></a><span data-ttu-id="bbd16-103">Didacticiel : Intégration d’Azure Active Directory à Ariba</span><span class="sxs-lookup"><span data-stu-id="bbd16-103">Tutorial: Azure Active Directory integration with Ariba</span></span>

<span data-ttu-id="bbd16-104">Dans ce didacticiel, vous apprendrez comment toointegrate Ariba avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bbd16-104">In this tutorial, you learn how toointegrate Ariba with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="bbd16-105">Intégration Ariba à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="bbd16-105">Integrating Ariba with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="bbd16-106">Vous pouvez contrôler dans Azure AD qui a accès tooAriba</span><span class="sxs-lookup"><span data-stu-id="bbd16-106">You can control in Azure AD who has access tooAriba</span></span>
- <span data-ttu-id="bbd16-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooAriba (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd16-107">You can enable your users tooautomatically get signed-on tooAriba (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="bbd16-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="bbd16-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="bbd16-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="bbd16-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bbd16-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="bbd16-110">Prerequisites</span></span>

<span data-ttu-id="bbd16-111">tooconfigure intégration d’Azure AD avec Ariba, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="bbd16-111">tooconfigure Azure AD integration with Ariba, you need hello following items:</span></span>

- <span data-ttu-id="bbd16-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd16-112">An Azure AD subscription</span></span>
- <span data-ttu-id="bbd16-113">Un abonnement Ariba pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="bbd16-113">An Ariba single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="bbd16-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="bbd16-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="bbd16-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="bbd16-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="bbd16-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="bbd16-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="bbd16-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bbd16-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="bbd16-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="bbd16-118">Scenario description</span></span>
<span data-ttu-id="bbd16-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="bbd16-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="bbd16-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="bbd16-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="bbd16-121">Ajout de Ariba à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bbd16-121">Adding Ariba from hello gallery</span></span>
2. <span data-ttu-id="bbd16-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd16-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-ariba-from-hello-gallery"></a><span data-ttu-id="bbd16-123">Ajout de Ariba à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="bbd16-123">Adding Ariba from hello gallery</span></span>
<span data-ttu-id="bbd16-124">tooconfigure hello intégration de Ariba dans Azure AD, vous devez tooadd Ariba à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="bbd16-124">tooconfigure hello integration of Ariba into Azure AD, you need tooadd Ariba from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="bbd16-125">**tooadd Ariba à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bbd16-125">**tooadd Ariba from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbd16-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bbd16-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="bbd16-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="bbd16-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="bbd16-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="bbd16-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="bbd16-133">Dans la zone de recherche de hello, tapez **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-133">In hello search box, type **Ariba**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_search.png)

5. <span data-ttu-id="bbd16-135">Dans le volet de résultats hello, sélectionnez **Ariba**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="bbd16-135">In hello results panel, select **Ariba**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="bbd16-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd16-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="bbd16-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec Ariba au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="bbd16-138">In this section, you configure and test Azure AD single sign-on with Ariba based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="bbd16-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello Ariba est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bbd16-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Ariba is tooa user in Azure AD.</span></span> <span data-ttu-id="bbd16-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Ariba doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="bbd16-140">In other words, a link relationship between an Azure AD user and hello related user in Ariba needs toobe established.</span></span>

<span data-ttu-id="bbd16-141">Dans Ariba, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="bbd16-141">In Ariba, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="bbd16-142">tooconfigure et test Azure AD l’authentification unique avec Ariba, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="bbd16-142">tooconfigure and test Azure AD single sign-on with Ariba, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="bbd16-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="bbd16-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="bbd16-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="bbd16-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="bbd16-145">**[Création d’un utilisateur de test Ariba](#creating-an-ariba-test-user)**  -toohave un équivalent de Britta Simon dans Ariba est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="bbd16-145">**[Creating an Ariba test user](#creating-an-ariba-test-user)** - toohave a counterpart of Britta Simon in Ariba that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="bbd16-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bbd16-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="bbd16-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="bbd16-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="bbd16-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd16-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="bbd16-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Ariba.</span><span class="sxs-lookup"><span data-stu-id="bbd16-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Ariba application.</span></span>

<span data-ttu-id="bbd16-150">**tooconfigure Azure AD single sign-on avec Ariba, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bbd16-150">**tooconfigure Azure AD single sign-on with Ariba, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbd16-151">Bonjour portail Azure, sur hello **Ariba** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-151">In hello Azure portal, on hello **Ariba** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="bbd16-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="bbd16-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_samlbase.png)

3. <span data-ttu-id="bbd16-155">Sur hello **Ariba domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bbd16-155">On hello **Ariba Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_url.png)

    <span data-ttu-id="bbd16-157">a.</span><span class="sxs-lookup"><span data-stu-id="bbd16-157">a.</span></span> <span data-ttu-id="bbd16-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle : `https://<subdomain>.sourcing.ariba.com` ou`https://<subdomain>.supplier.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="bbd16-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<subdomain>.sourcing.ariba.com` or `https://<subdomain>.supplier.ariba.com`</span></span>

    <span data-ttu-id="bbd16-159">b.</span><span class="sxs-lookup"><span data-stu-id="bbd16-159">b.</span></span> <span data-ttu-id="bbd16-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`http://<subdomain>.procurement-2.ariba.com`</span><span class="sxs-lookup"><span data-stu-id="bbd16-160">In hello **Identifier** textbox, type a URL using hello following pattern: `http://<subdomain>.procurement-2.ariba.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="bbd16-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="bbd16-161">These values are not real.</span></span> <span data-ttu-id="bbd16-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="bbd16-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="bbd16-163">Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur.</span><span class="sxs-lookup"><span data-stu-id="bbd16-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="bbd16-164">Contactez l’équipe du support Client de Ariba **1-866-218-2155** tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="bbd16-164">Contact Ariba Client support team at **1-866-218-2155** tooget these values.</span></span> 
 

4. <span data-ttu-id="bbd16-165">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="bbd16-165">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate  file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_certificate.png) 

5. <span data-ttu-id="bbd16-167">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="bbd16-167">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ariba-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="bbd16-169">tooget l’authentification unique configurée pour votre application, d’appeler l’équipe de support Ariba sur **1-866-218-2155** et ils allez faciliter davantage sur le mode de téléchargement tooprovide les hello **certificat (Base64)** fichier.</span><span class="sxs-lookup"><span data-stu-id="bbd16-169">tooget SSO configured for your application, call Ariba support team on **1-866-218-2155** and they'll assist you further on how tooprovide them hello downloaded **Certificate (Base64)** file.</span></span>  
 
> [!TIP]
> <span data-ttu-id="bbd16-170">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="bbd16-170">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="bbd16-171">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="bbd16-171">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="bbd16-172">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="bbd16-172">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="bbd16-173">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd16-173">Creating an Azure AD test user</span></span>
<span data-ttu-id="bbd16-174">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="bbd16-174">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="bbd16-176">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bbd16-176">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbd16-177">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="bbd16-177">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="bbd16-179">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-179">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="bbd16-181">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="bbd16-181">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="bbd16-183">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="bbd16-183">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-ariba-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="bbd16-185">a.</span><span class="sxs-lookup"><span data-stu-id="bbd16-185">a.</span></span> <span data-ttu-id="bbd16-186">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-186">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="bbd16-187">b.</span><span class="sxs-lookup"><span data-stu-id="bbd16-187">b.</span></span> <span data-ttu-id="bbd16-188">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="bbd16-188">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="bbd16-189">c.</span><span class="sxs-lookup"><span data-stu-id="bbd16-189">c.</span></span> <span data-ttu-id="bbd16-190">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-190">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="bbd16-191">d.</span><span class="sxs-lookup"><span data-stu-id="bbd16-191">d.</span></span> <span data-ttu-id="bbd16-192">Cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-192">Click **Create**.</span></span>
 
### <a name="creating-an-ariba-test-user"></a><span data-ttu-id="bbd16-193">Création d’un utilisateur de test Ariba</span><span class="sxs-lookup"><span data-stu-id="bbd16-193">Creating an Ariba test user</span></span>

<span data-ttu-id="bbd16-194">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon dans Ariba.</span><span class="sxs-lookup"><span data-stu-id="bbd16-194">hello objective of this section is toocreate a user called Britta Simon in Ariba.</span></span> <span data-ttu-id="bbd16-195">Travailler avec l’équipe de support Ariba **1-866-218-2155** tooadd les utilisateurs de hello Bonjour Ariba système.</span><span class="sxs-lookup"><span data-stu-id="bbd16-195">Work with Ariba support team at **1-866-218-2155** tooadd hello users in hello Ariba system.</span></span> 

 >[!NOTE]
 ><span data-ttu-id="bbd16-196">Si vous devez manuellement toocreate un utilisateur, vous devez toocontact hello Ariba équipe de support **1-866-218-2155**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-196">If you need toocreate a user manually, you need toocontact hello Ariba support team at **1-866-218-2155**.</span></span>
 >  

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="bbd16-197">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="bbd16-197">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="bbd16-198">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooAriba.</span><span class="sxs-lookup"><span data-stu-id="bbd16-198">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooAriba.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="bbd16-200">**tooassign Britta Simon tooAriba, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="bbd16-200">**tooassign Britta Simon tooAriba, perform hello following steps:**</span></span>

1. <span data-ttu-id="bbd16-201">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-201">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="bbd16-203">Dans la liste des applications hello, sélectionnez **Ariba**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-203">In hello applications list, select **Ariba**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-ariba-tutorial/tutorial_ariba_app.png) 

3. <span data-ttu-id="bbd16-205">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-205">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="bbd16-207">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-207">Click **Add** button.</span></span> <span data-ttu-id="bbd16-208">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-208">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="bbd16-210">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="bbd16-210">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="bbd16-211">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-211">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="bbd16-212">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="bbd16-212">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="bbd16-213">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="bbd16-213">Testing single sign-on</span></span>
<span data-ttu-id="bbd16-214">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="bbd16-214">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="bbd16-215">Lorsque vous cliquez sur mosaïque Ariba hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Ariba application.</span><span class="sxs-lookup"><span data-stu-id="bbd16-215">When you click hello Ariba tile in hello Access Panel, you should get automatically signed-on tooyour Ariba application.</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="bbd16-216">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="bbd16-216">Additional resources</span></span>

* [<span data-ttu-id="bbd16-217">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbd16-217">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="bbd16-218">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="bbd16-218">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-ariba-tutorial/tutorial_general_203.png

