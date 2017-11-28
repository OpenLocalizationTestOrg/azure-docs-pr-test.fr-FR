---
title: "Didacticiel : Intégration d'Azure Active Directory avec Datahug | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et Datahug."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 5c0dc1ea-7ff4-4554-b60b-0f2fa9f5abaa
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: jeedes
ms.openlocfilehash: 79ccb939c7a19720bcf696af141f747db00c8a2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-datahug"></a><span data-ttu-id="68cc3-103">Didacticiel : Intégration d’Azure Active Directory avec Datahug</span><span class="sxs-lookup"><span data-stu-id="68cc3-103">Tutorial: Azure Active Directory integration with Datahug</span></span>

<span data-ttu-id="68cc3-104">Dans ce didacticiel, vous apprendrez comment toointegrate Datahug avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="68cc3-104">In this tutorial, you learn how toointegrate Datahug with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="68cc3-105">Intégration Datahug à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="68cc3-105">Integrating Datahug with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="68cc3-106">Vous pouvez contrôler dans Azure AD qui a accès tooDatahug</span><span class="sxs-lookup"><span data-stu-id="68cc3-106">You can control in Azure AD who has access tooDatahug</span></span>
- <span data-ttu-id="68cc3-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooDatahug (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="68cc3-107">You can enable your users tooautomatically get signed-on tooDatahug (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="68cc3-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="68cc3-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="68cc3-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez.</span><span class="sxs-lookup"><span data-stu-id="68cc3-109">If you want tooknow more details about SaaS app integration with Azure AD, see.</span></span> <span data-ttu-id="68cc3-110">[Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="68cc3-110">[What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="68cc3-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="68cc3-111">Prerequisites</span></span>

<span data-ttu-id="68cc3-112">tooconfigure intégration d’Azure AD avec Datahug, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="68cc3-112">tooconfigure Azure AD integration with Datahug, you need hello following items:</span></span>

- <span data-ttu-id="68cc3-113">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="68cc3-113">An Azure AD subscription</span></span>
- <span data-ttu-id="68cc3-114">Un abonnement Datahug pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="68cc3-114">A Datahug single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="68cc3-115">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="68cc3-115">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="68cc3-116">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="68cc3-116">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="68cc3-117">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="68cc3-117">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="68cc3-118">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="68cc3-118">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="68cc3-119">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="68cc3-119">Scenario description</span></span>
<span data-ttu-id="68cc3-120">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="68cc3-120">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="68cc3-121">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="68cc3-121">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="68cc3-122">Ajout de Datahug à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="68cc3-122">Adding Datahug from hello gallery</span></span>
2. <span data-ttu-id="68cc3-123">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="68cc3-123">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-datahug-from-hello-gallery"></a><span data-ttu-id="68cc3-124">Ajout de Datahug à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="68cc3-124">Adding Datahug from hello gallery</span></span>
<span data-ttu-id="68cc3-125">intégration de hello tooconfigure de Datahug dans Azure AD, vous devez tooadd Datahug à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="68cc3-125">tooconfigure hello integration of Datahug into Azure AD, you need tooadd Datahug from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="68cc3-126">**tooadd Datahug à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="68cc3-126">**tooadd Datahug from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="68cc3-127">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="68cc3-127">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="68cc3-129">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-129">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="68cc3-130">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-130">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="68cc3-132">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="68cc3-132">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="68cc3-134">Dans la zone de recherche de hello, tapez **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-134">In hello search box, type **Datahug**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_search.png)

5. <span data-ttu-id="68cc3-136">Dans le volet de résultats hello, sélectionnez **Datahug**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="68cc3-136">In hello results panel, select **Datahug**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="68cc3-138">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="68cc3-138">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="68cc3-139">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Datahug, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="68cc3-139">In this section, you configure and test Azure AD single sign-on with Datahug based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="68cc3-140">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Datahug est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="68cc3-140">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Datahug is tooa user in Azure AD.</span></span> <span data-ttu-id="68cc3-141">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Datahug doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="68cc3-141">In other words, a link relationship between an Azure AD user and hello related user in Datahug needs toobe established.</span></span>

<span data-ttu-id="68cc3-142">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Datahug.</span><span class="sxs-lookup"><span data-stu-id="68cc3-142">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Datahug.</span></span>

<span data-ttu-id="68cc3-143">tooconfigure et test Azure AD l’authentification unique avec Datahug, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="68cc3-143">tooconfigure and test Azure AD single sign-on with Datahug, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="68cc3-144">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="68cc3-144">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="68cc3-145">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="68cc3-145">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="68cc3-146">**[Création d’un utilisateur de test Datahug](#creating-a-datahug-test-user)**  -toohave un équivalent de Britta Simon dans Datahug est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="68cc3-146">**[Creating a Datahug test user](#creating-a-datahug-test-user)** - toohave a counterpart of Britta Simon in Datahug that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="68cc3-147">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="68cc3-147">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="68cc3-148">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="68cc3-148">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="68cc3-149">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="68cc3-149">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="68cc3-150">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application Datahug.</span><span class="sxs-lookup"><span data-stu-id="68cc3-150">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Datahug application.</span></span>

<span data-ttu-id="68cc3-151">**tooconfigure Azure AD single sign-on avec Datahug, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="68cc3-151">**tooconfigure Azure AD single sign-on with Datahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="68cc3-152">Bonjour portail Azure, sur hello **Datahug** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-152">In hello Azure portal, on hello **Datahug** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="68cc3-154">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="68cc3-154">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_samlbase.png)

3. <span data-ttu-id="68cc3-156">Sur hello **Datahug domaine et les URL** section, si vous le souhaitez application hello tooconfigure **IDP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="68cc3-156">On hello **Datahug Domain and URLs** section, If you wish tooconfigure hello application in **IDP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_ur1.png)

    <span data-ttu-id="68cc3-158">a.</span><span class="sxs-lookup"><span data-stu-id="68cc3-158">a.</span></span> <span data-ttu-id="68cc3-159">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://apps.datahug.com/identity/<uniqueID>`</span><span class="sxs-lookup"><span data-stu-id="68cc3-159">In hello **Identifier** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>`</span></span>

    <span data-ttu-id="68cc3-160">b.</span><span class="sxs-lookup"><span data-stu-id="68cc3-160">b.</span></span> <span data-ttu-id="68cc3-161">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://apps.datahug.com/identity/<uniqueID>/acs`</span><span class="sxs-lookup"><span data-stu-id="68cc3-161">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://apps.datahug.com/identity/<uniqueID>/acs`</span></span>

4. <span data-ttu-id="68cc3-162">Cliquez sur **Afficher les paramètres d’URL avancés**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-162">Check **Show advanced URL settings**.</span></span> <span data-ttu-id="68cc3-163">Si vous le souhaitez application hello tooconfigure **SP** en mode initié par :</span><span class="sxs-lookup"><span data-stu-id="68cc3-163">If you wish tooconfigure hello application in **SP** initiated mode:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_url2.png)

    <span data-ttu-id="68cc3-165">Bonjour **URL de connexion** zone de texte, tapez une URL en tant que :`https://apps.datahug.com/`</span><span class="sxs-lookup"><span data-stu-id="68cc3-165">In hello **Sign-on URL** textbox, type a URL as: `https://apps.datahug.com/`</span></span>
     
    > [!NOTE] 
    > <span data-ttu-id="68cc3-166">Ces valeurs ne sont pas hello réel.</span><span class="sxs-lookup"><span data-stu-id="68cc3-166">These values are not hello real.</span></span> <span data-ttu-id="68cc3-167">Mettre à jour ces valeurs hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="68cc3-167">Update these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="68cc3-168">Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur et l’URL de réponse.</span><span class="sxs-lookup"><span data-stu-id="68cc3-168">Here we suggest you toouse hello unique value of string in hello Identifier and Reply URL.</span></span> <span data-ttu-id="68cc3-169">Contact [équipe de support Client de Datahug](http://datahug.com/about/contact-us/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="68cc3-169">Contact [Datahug Client support team](http://datahug.com/about/contact-us/) tooget these values.</span></span> 

5. <span data-ttu-id="68cc3-170">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="68cc3-170">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_certificate.png) 

6.  <span data-ttu-id="68cc3-172">Vérifiez **« Afficher les paramètres de signature de certificat avancées »** et effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="68cc3-172">Check **“Show advanced certificate signing settings”** and perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_cert.png)

    <span data-ttu-id="68cc3-174">a.</span><span class="sxs-lookup"><span data-stu-id="68cc3-174">a.</span></span> <span data-ttu-id="68cc3-175">Dans **Option de signature**, sélectionnez **Signer l’assertion SAML**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-175">In **Signing Option**, select **Sign SAML assertion**.</span></span>
    
    <span data-ttu-id="68cc3-176">b.</span><span class="sxs-lookup"><span data-stu-id="68cc3-176">b.</span></span> <span data-ttu-id="68cc3-177">Dans **Algorithme de signature**, sélectionnez **SHA1**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-177">In **Signing algorithm**, select **SHA1**.</span></span>
 
7. <span data-ttu-id="68cc3-178">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="68cc3-178">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_general_400.png)
    
8. <span data-ttu-id="68cc3-180">Sur hello **Datahug Configuration** , cliquez sur **Datahug de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="68cc3-180">On hello **Datahug Configuration** section, click **Configure Datahug** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="68cc3-181">Hello de copie **ID d’entité SAML** et **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="68cc3-181">Copy hello **SAML Entity ID** and **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_configure.png) 

9. <span data-ttu-id="68cc3-183">tooconfigure l’authentification unique sur **Datahug** côté, vous devez hello toosend téléchargé **Metadata XML**, **ID d’entité SAML** et **SAML Single Sign-On Service URL** trop[prise en charge Datahug](http://datahug.com/about/contact-us/).</span><span class="sxs-lookup"><span data-stu-id="68cc3-183">tooconfigure single sign-on on **Datahug** side, you need toosend hello downloaded **Metadata XML**, **SAML Entity ID** and **SAML Single Sign-On Service URL** too[Datahug support](http://datahug.com/about/contact-us/).</span></span> <span data-ttu-id="68cc3-184">Ils définir cette application toohave hello connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="68cc3-184">They set this application up toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="68cc3-185">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="68cc3-185">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="68cc3-186">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="68cc3-186">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="68cc3-187">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="68cc3-187">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="68cc3-188">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="68cc3-188">Creating an Azure AD test user</span></span>
<span data-ttu-id="68cc3-189">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="68cc3-189">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="68cc3-191">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="68cc3-191">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="68cc3-192">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="68cc3-192">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="68cc3-194">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-194">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="68cc3-196">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="68cc3-196">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="68cc3-198">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="68cc3-198">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-datahug-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="68cc3-200">a.</span><span class="sxs-lookup"><span data-stu-id="68cc3-200">a.</span></span> <span data-ttu-id="68cc3-201">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-201">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="68cc3-202">b.</span><span class="sxs-lookup"><span data-stu-id="68cc3-202">b.</span></span> <span data-ttu-id="68cc3-203">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="68cc3-203">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="68cc3-204">c.</span><span class="sxs-lookup"><span data-stu-id="68cc3-204">c.</span></span> <span data-ttu-id="68cc3-205">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-205">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="68cc3-206">d.</span><span class="sxs-lookup"><span data-stu-id="68cc3-206">d.</span></span> <span data-ttu-id="68cc3-207">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-207">Click **Create**.</span></span>
 
### <a name="creating-a-datahug-test-user"></a><span data-ttu-id="68cc3-208">Création d’un utilisateur de test Datahug</span><span class="sxs-lookup"><span data-stu-id="68cc3-208">Creating a Datahug test user</span></span>

<span data-ttu-id="68cc3-209">tooenable Azure AD les utilisateurs toolog dans tooDatahug, vous devez les configurer dans Datahug.</span><span class="sxs-lookup"><span data-stu-id="68cc3-209">tooenable Azure AD users toolog in tooDatahug, they must be provisioned into Datahug.</span></span>  
<span data-ttu-id="68cc3-210">Pour Datahug, l’approvisionnement est une tâche manuelle.</span><span class="sxs-lookup"><span data-stu-id="68cc3-210">When Datahug, provisioning is a manual task.</span></span>

<span data-ttu-id="68cc3-211">**tooprovision un compte d’utilisateur, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="68cc3-211">**tooprovision a user account, perform hello following steps:**</span></span>

1. <span data-ttu-id="68cc3-212">Ouvrez une session dans tooyour Datahug site d’entreprise en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="68cc3-212">Log in tooyour Datahug company site as an administrator.</span></span>

2. <span data-ttu-id="68cc3-213">Placez le curseur sur hello **représentant une roue dentée** dans le coin supérieur droit de hello et cliquez sur **paramètres**</span><span class="sxs-lookup"><span data-stu-id="68cc3-213">Hover over hello **cog** in hello top right-hand corner and click **Settings**</span></span>
   
   ![Ajouter un employé](./media/active-directory-saas-datahug-tutorial/1.png)

3. <span data-ttu-id="68cc3-215">Choisissez **personnes** et cliquez sur hello **ajouter des utilisateurs** onglet</span><span class="sxs-lookup"><span data-stu-id="68cc3-215">Choose **People** and click hello **Add Users** tab</span></span>

    ![Ajouter un employé](./media/active-directory-saas-datahug-tutorial/2.png)

4. <span data-ttu-id="68cc3-217">Tapez messagerie hello de personne hello vous aimeriez toocreate un compte pour sur **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-217">Type hello email of hello person you would like toocreate an account for and click **Add**.</span></span>

    ![Ajouter un employé](./media/active-directory-saas-datahug-tutorial/3.png)

    > [!NOTE] 
    > <span data-ttu-id="68cc3-219">Vous pouvez envoyer toouser de messagerie de l’inscription en sélectionnant **envoyer le message électronique de Bienvenue** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="68cc3-219">You can send registration mail toouser by selecting **Send welcome email** checkbox.</span></span>  
    > <span data-ttu-id="68cc3-220">Si vous créez un compte pour Salesforce ne pas envoyer de message électronique de bienvenue hello.</span><span class="sxs-lookup"><span data-stu-id="68cc3-220">If you are creating an account for Salesforce do not send hello welcome email.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="68cc3-221">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="68cc3-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="68cc3-222">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooDatahug.</span><span class="sxs-lookup"><span data-stu-id="68cc3-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooDatahug.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="68cc3-224">**tooassign Britta Simon tooDatahug, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="68cc3-224">**tooassign Britta Simon tooDatahug, perform hello following steps:**</span></span>

1. <span data-ttu-id="68cc3-225">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-225">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="68cc3-227">Dans la liste des applications hello, sélectionnez **Datahug**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-227">In hello applications list, select **Datahug**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-datahug-tutorial/tutorial_datahug_app.png) 

3. <span data-ttu-id="68cc3-229">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="68cc3-231">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-231">Click **Add** button.</span></span> <span data-ttu-id="68cc3-232">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="68cc3-234">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="68cc3-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="68cc3-235">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="68cc3-236">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="68cc3-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="68cc3-237">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="68cc3-237">Testing single sign-on</span></span>

<span data-ttu-id="68cc3-238">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="68cc3-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>
<span data-ttu-id="68cc3-239">Lorsque vous cliquez sur mosaïque Datahug hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour Datahug application.</span><span class="sxs-lookup"><span data-stu-id="68cc3-239">When you click hello Datahug tile in hello Access Panel, you should get automatically signed-on tooyour Datahug application.</span></span> <span data-ttu-id="68cc3-240">Pour plus d’informations sur le panneau d’accès, consultez [Présentation du panneau d’accès](https://msdn.microsoft.com/library/dn308586).</span><span class="sxs-lookup"><span data-stu-id="68cc3-240">For more information about the Access Panel, see [Introduction to the Access Panel](https://msdn.microsoft.com/library/dn308586).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="68cc3-241">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="68cc3-241">Additional resources</span></span>

* [<span data-ttu-id="68cc3-242">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="68cc3-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="68cc3-243">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="68cc3-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-datahug-tutorial/tutorial_general_203.png

