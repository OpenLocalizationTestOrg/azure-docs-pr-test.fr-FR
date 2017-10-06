---
title: "Didacticiel : Intégration d’Azure Active Directory à Halogen Software | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et halogène logiciel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ca2298d-9a0c-4f14-925c-fa23f2659d28
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: bdb67de713771d6e306f287c4b13895f6336f7ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-halogen-software"></a><span data-ttu-id="4cb37-103">Didacticiel : Intégration d’Azure Active Directory avec Halogen Software</span><span class="sxs-lookup"><span data-stu-id="4cb37-103">Tutorial: Azure Active Directory integration with Halogen Software</span></span>

<span data-ttu-id="4cb37-104">Dans ce didacticiel, vous apprendrez comment toointegrate logiciel halogène avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4cb37-104">In this tutorial, you learn how toointegrate Halogen Software with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4cb37-105">Intégration du logiciel de halogène avec Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4cb37-105">Integrating Halogen Software with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="4cb37-106">Vous pouvez contrôler dans Azure AD qui a accès tooHalogen logiciel</span><span class="sxs-lookup"><span data-stu-id="4cb37-106">You can control in Azure AD who has access tooHalogen Software</span></span>
- <span data-ttu-id="4cb37-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooHalogen logiciels (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="4cb37-107">You can enable your users tooautomatically get signed-on tooHalogen Software (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="4cb37-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4cb37-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="4cb37-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4cb37-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4cb37-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4cb37-110">Prerequisites</span></span>

<span data-ttu-id="4cb37-111">tooconfigure intégration d’Azure AD avec halogène logiciel, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4cb37-111">tooconfigure Azure AD integration with Halogen Software, you need hello following items:</span></span>

- <span data-ttu-id="4cb37-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4cb37-112">An Azure AD subscription</span></span>
- <span data-ttu-id="4cb37-113">Un abonnement Halogen Software pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4cb37-113">A Halogen Software single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="4cb37-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="4cb37-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="4cb37-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="4cb37-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="4cb37-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4cb37-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="4cb37-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4cb37-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="4cb37-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4cb37-118">Scenario description</span></span>

<span data-ttu-id="4cb37-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4cb37-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4cb37-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="4cb37-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="4cb37-121">Ajout d’un logiciel de halogène à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4cb37-121">Adding Halogen Software from hello gallery</span></span>
2. <span data-ttu-id="4cb37-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4cb37-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-halogen-software-from-hello-gallery"></a><span data-ttu-id="4cb37-123">Ajout d’un logiciel de halogène à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="4cb37-123">Adding Halogen Software from hello gallery</span></span>

<span data-ttu-id="4cb37-124">tooconfigure hello intégration des logiciels de halogène dans Azure AD, vous devez tooadd halogène logiciel à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4cb37-124">tooconfigure hello integration of Halogen Software into Azure AD, you need tooadd Halogen Software from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="4cb37-125">**tooadd logiciel halogène à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4cb37-125">**tooadd Halogen Software from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="4cb37-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4cb37-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4cb37-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="4cb37-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4cb37-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4cb37-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4cb37-133">Dans la zone de recherche de hello, tapez **halogène logiciel**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-133">In hello search box, type **Halogen Software**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_search.png)

5. <span data-ttu-id="4cb37-135">Dans le volet de résultats hello, sélectionnez **halogène logiciel**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="4cb37-135">In hello results panel, select **Halogen Software**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="4cb37-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4cb37-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="4cb37-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Halogen Software à l’aide d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4cb37-138">In this section, you configure and test Azure AD single sign-on with Halogen Software based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="4cb37-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello halogène logiciel est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4cb37-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Halogen Software is tooa user in Azure AD.</span></span> <span data-ttu-id="4cb37-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur dans le logiciel de halogène hello doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="4cb37-140">In other words, a link relationship between an Azure AD user and hello related user in Halogen Software needs toobe established.</span></span>

<span data-ttu-id="4cb37-141">Dans le logiciel de HALOGÈNE, affecter la valeur de hello de hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="4cb37-141">In Halogen Software, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="4cb37-142">tooconfigure et test Azure AD l’authentification unique avec halogène logiciel, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="4cb37-142">tooconfigure and test Azure AD single sign-on with Halogen Software, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="4cb37-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4cb37-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="4cb37-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4cb37-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4cb37-145">**[Création d’un utilisateur de test halogène logiciel](#creating-a-halogen-software-test-user)**  -toohave un équivalent de Britta Simon à halogène un logiciel qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4cb37-145">**[Creating a Halogen Software test user](#creating-a-halogen-software-test-user)** - toohave a counterpart of Britta Simon in Halogen Software that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="4cb37-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4cb37-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4cb37-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="4cb37-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="4cb37-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4cb37-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="4cb37-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application halogène.</span><span class="sxs-lookup"><span data-stu-id="4cb37-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your Halogen Software application.</span></span>

<span data-ttu-id="4cb37-150">**tooconfigure Azure AD authentification unique avec le logiciel de HALOGÈNE, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4cb37-150">**tooconfigure Azure AD single sign-on with Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="4cb37-151">Bonjour portail Azure, sur hello **halogène logiciel** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-151">In hello Azure portal, on hello **Halogen Software** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4cb37-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4cb37-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_samlbase.png)

3. <span data-ttu-id="4cb37-155">Sur hello **halogène logiciel domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4cb37-155">On hello **Halogen Software Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_url.png)

    <span data-ttu-id="4cb37-157">a.</span><span class="sxs-lookup"><span data-stu-id="4cb37-157">a.</span></span> <span data-ttu-id="4cb37-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="4cb37-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://global.hgncloud.com/<companyname>`</span></span>

    <span data-ttu-id="4cb37-159">b.</span><span class="sxs-lookup"><span data-stu-id="4cb37-159">b.</span></span> <span data-ttu-id="4cb37-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle : `https://global.halogensoftware.com/<companyname>`,`https://global.hgncloud.com/<companyname>`</span><span class="sxs-lookup"><span data-stu-id="4cb37-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://global.halogensoftware.com/<companyname>`, `https://global.hgncloud.com/<companyname>`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4cb37-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="4cb37-161">These values are not real.</span></span> <span data-ttu-id="4cb37-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="4cb37-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="4cb37-163">Contact [équipe de support Client de logiciel halogène](https://support.halogensoftware.com/) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="4cb37-163">Contact [Halogen Software Client support team](https://support.halogensoftware.com/) tooget these values.</span></span> 
 


4. <span data-ttu-id="4cb37-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4cb37-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_certificate.png) 

5. <span data-ttu-id="4cb37-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="4cb37-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="4cb37-168">Dans une autre fenêtre de navigateur, l’authentification tooyour **halogène logiciel** application en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4cb37-168">In a different browser window, sign-on tooyour **Halogen Software** application as an administrator.</span></span>

7. <span data-ttu-id="4cb37-169">Cliquez sur hello **Options** onglet.</span><span class="sxs-lookup"><span data-stu-id="4cb37-169">Click hello **Options** tab.</span></span> 
   
    ![Qu’est-ce qu’Azure AD Connect ?][12]

8. <span data-ttu-id="4cb37-171">Dans le volet de navigation gauche hello, cliquez sur **Configuration SAML**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-171">In hello left navigation pane, click **SAML Configuration**.</span></span> 
   
    ![Qu’est-ce qu’Azure AD Connect ?][13]

9. <span data-ttu-id="4cb37-173">Sur hello **Configuration SAML** page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4cb37-173">On hello **SAML Configuration** page, perform hello following steps:</span></span> 

    ![Qu’est-ce qu’Azure AD Connect ?][14]

     <span data-ttu-id="4cb37-175">a.</span><span class="sxs-lookup"><span data-stu-id="4cb37-175">a.</span></span> <span data-ttu-id="4cb37-176">Dans **Unique Identifier** (Identificateur unique), sélectionnez **NameID**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-176">As **Unique Identifier**, select **NameID**.</span></span>

     <span data-ttu-id="4cb37-177">b.</span><span class="sxs-lookup"><span data-stu-id="4cb37-177">b.</span></span> <span data-ttu-id="4cb37-178">Dans **Unique Identifier Maps To** (l’identificateur unique mappe vers), sélectionnez **Username** (Nom d’utilisateur).</span><span class="sxs-lookup"><span data-stu-id="4cb37-178">As **Unique Identifier Maps To**, select **Username**.</span></span>
  
     <span data-ttu-id="4cb37-179">c.</span><span class="sxs-lookup"><span data-stu-id="4cb37-179">c.</span></span> <span data-ttu-id="4cb37-180">tooupload votre fichier de métadonnées téléchargé, cliquez sur **Parcourir** tooselect fichier hello, puis **télécharger le fichier**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-180">tooupload your downloaded metadata file, click **Browse** tooselect hello file, and then **Upload File**.</span></span>
 
     <span data-ttu-id="4cb37-181">d.</span><span class="sxs-lookup"><span data-stu-id="4cb37-181">d.</span></span> <span data-ttu-id="4cb37-182">configuration de hello tootest, cliquez sur **exécuter le Test**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-182">tootest hello configuration, click **Run Test**.</span></span> 
    
    >[!NOTE]
    ><span data-ttu-id="4cb37-183">Vous devez toowait pour le message de type hello »*hello SAML test est terminé. Please close this window* » s’affiche.</span><span class="sxs-lookup"><span data-stu-id="4cb37-183">You need toowait for hello message "*hello SAML test is complete. Please close this window*".</span></span> <span data-ttu-id="4cb37-184">Ensuite, fermez hello ouvert fenêtre du navigateur.</span><span class="sxs-lookup"><span data-stu-id="4cb37-184">Then, close hello opened browser window.</span></span> <span data-ttu-id="4cb37-185">Hello **SAML d’activer** case à cocher est activée uniquement si le test de hello a été effectuée.</span><span class="sxs-lookup"><span data-stu-id="4cb37-185">hello **Enable SAML** checkbox is only enabled if hello test has been completed.</span></span> 
     
     <span data-ttu-id="4cb37-186">e.</span><span class="sxs-lookup"><span data-stu-id="4cb37-186">e.</span></span> <span data-ttu-id="4cb37-187">Sélectionnez **Enable SAML**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-187">Select **Enable SAML**.</span></span>
    
     <span data-ttu-id="4cb37-188">f.</span><span class="sxs-lookup"><span data-stu-id="4cb37-188">f.</span></span> <span data-ttu-id="4cb37-189">Cliquez sur **Enregistrer les modifications**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-189">Click **Save Changes**.</span></span> 

> [!TIP]
> <span data-ttu-id="4cb37-190">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="4cb37-190">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="4cb37-191">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="4cb37-191">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="4cb37-192">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="4cb37-192">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="4cb37-193">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4cb37-193">Creating an Azure AD test user</span></span>

<span data-ttu-id="4cb37-194">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="4cb37-194">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="4cb37-196">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4cb37-196">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="4cb37-197">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="4cb37-197">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4cb37-199">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-199">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4cb37-201">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="4cb37-201">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4cb37-203">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4cb37-203">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-halogen-software-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4cb37-205">a.</span><span class="sxs-lookup"><span data-stu-id="4cb37-205">a.</span></span> <span data-ttu-id="4cb37-206">Bonjour **nom** zone de texte, nom du type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-206">In hello **Name** textbox, type name as **BrittaSimon**.</span></span>

    <span data-ttu-id="4cb37-207">b.</span><span class="sxs-lookup"><span data-stu-id="4cb37-207">b.</span></span> <span data-ttu-id="4cb37-208">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="4cb37-208">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4cb37-209">c.</span><span class="sxs-lookup"><span data-stu-id="4cb37-209">c.</span></span> <span data-ttu-id="4cb37-210">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-210">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="4cb37-211">d.</span><span class="sxs-lookup"><span data-stu-id="4cb37-211">d.</span></span> <span data-ttu-id="4cb37-212">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-212">Click **Create**.</span></span>
 
### <a name="creating-a-halogen-software-test-user"></a><span data-ttu-id="4cb37-213">Création d’un utilisateur de test Halogen Software</span><span class="sxs-lookup"><span data-stu-id="4cb37-213">Creating a Halogen Software test user</span></span>

<span data-ttu-id="4cb37-214">objectif Hello de cette section est toocreate un utilisateur appelé Britta Simon halogène logiciel.</span><span class="sxs-lookup"><span data-stu-id="4cb37-214">hello objective of this section is toocreate a user called Britta Simon in Halogen Software.</span></span>

<span data-ttu-id="4cb37-215">**toocreate un utilisateur appelé Britta Simon halogène logiciel, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4cb37-215">**toocreate a user called Britta Simon in Halogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="4cb37-216">Ouverture de session tooyour **halogène logiciel** application en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="4cb37-216">Sign on tooyour **Halogen Software** application as an administrator.</span></span>

2. <span data-ttu-id="4cb37-217">Cliquez sur hello **Centre utilisateur** onglet, puis cliquez sur **Create User**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-217">Click hello **User Center** tab, and then click **Create User**.</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][300]  

3. <span data-ttu-id="4cb37-219">Sur hello **nouvel utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="4cb37-219">On hello **New User** dialog page, perform hello following steps:</span></span>
   
    ![Qu’est-ce qu’Azure AD Connect ?][301]

    <span data-ttu-id="4cb37-221">a.</span><span class="sxs-lookup"><span data-stu-id="4cb37-221">a.</span></span> <span data-ttu-id="4cb37-222">Bonjour **prénom** zone de texte, type prénom utilisateur hello comme **Brian**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-222">In hello **First Name** textbox, type first name of hello user like **Britta**.</span></span>
    
    <span data-ttu-id="4cb37-223">b.</span><span class="sxs-lookup"><span data-stu-id="4cb37-223">b.</span></span> <span data-ttu-id="4cb37-224">Bonjour **nom** zone de texte, nom d’utilisateur hello comme type **Simon**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-224">In hello **Last Name** textbox, type last name of hello user like **Simon**.</span></span> 

    <span data-ttu-id="4cb37-225">c.</span><span class="sxs-lookup"><span data-stu-id="4cb37-225">c.</span></span> <span data-ttu-id="4cb37-226">Bonjour **nom d’utilisateur** zone de texte, type **Britta Simon**, nom d’utilisateur hello comme hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4cb37-226">In hello **Username** textbox, type **Britta Simon**, hello user name as in hello Azure portal.</span></span>

    <span data-ttu-id="4cb37-227">d.</span><span class="sxs-lookup"><span data-stu-id="4cb37-227">d.</span></span> <span data-ttu-id="4cb37-228">Bonjour **mot de passe** zone de texte, tapez un mot de passe pour Brian.</span><span class="sxs-lookup"><span data-stu-id="4cb37-228">In hello **Password** textbox, type a password for Britta.</span></span>
    
    <span data-ttu-id="4cb37-229">e.</span><span class="sxs-lookup"><span data-stu-id="4cb37-229">e.</span></span> <span data-ttu-id="4cb37-230">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-230">Click **Save**.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="4cb37-231">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="4cb37-231">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="4cb37-232">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooHalogen logiciel.</span><span class="sxs-lookup"><span data-stu-id="4cb37-232">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooHalogen Software.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="4cb37-234">**tooassign Britta Simon tooHalogen logiciel, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="4cb37-234">**tooassign Britta Simon tooHalogen Software, perform hello following steps:**</span></span>

1. <span data-ttu-id="4cb37-235">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-235">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4cb37-237">Dans la liste des applications hello, sélectionnez **halogène logiciel**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-237">In hello applications list, select **Halogen Software**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-halogen-software-tutorial/tutorial_halogensoftware_app.png) 

3. <span data-ttu-id="4cb37-239">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-239">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="4cb37-241">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-241">Click **Add** button.</span></span> <span data-ttu-id="4cb37-242">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-242">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="4cb37-244">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="4cb37-244">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="4cb37-245">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-245">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="4cb37-246">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="4cb37-246">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="4cb37-247">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4cb37-247">Testing single sign-on</span></span>

<span data-ttu-id="4cb37-248">objectif Hello de cette section est tootest votre configuration de l’authentification unique de Azure AD à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="4cb37-248">hello objective of this section is tootest your Azure AD SSO configuration using hello Access Panel.</span></span>

<span data-ttu-id="4cb37-249">Lorsque vous cliquez sur mosaïque halogène logiciel hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour halogène programme.</span><span class="sxs-lookup"><span data-stu-id="4cb37-249">When you click hello Halogen Software tile in hello Access Panel, you should get automatically signed-on tooyour Halogen Software application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4cb37-250">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4cb37-250">Additional resources</span></span>

* [<span data-ttu-id="4cb37-251">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4cb37-251">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4cb37-252">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4cb37-252">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_04.png

[12]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_12.png

[13]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_13.png

[14]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_14.png

[100]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_general_203.png

[300]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_300.png

[301]: ./media/active-directory-saas-halogen-software-tutorial/tutorial_halogen_301.png
