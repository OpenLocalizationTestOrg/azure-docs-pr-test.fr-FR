---
title: "Didacticiel : Intégration d’Azure Active Directory à FreshGrade | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et FreshGrade."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 1055bba6-f4df-462e-bc9b-1ad5ada0f638
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2017
ms.author: jeedes
ms.openlocfilehash: e2fe7cedd45290945ec5624453a9675abdd7726d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-freshgrade"></a><span data-ttu-id="2bc42-103">Didacticiel : Intégration d’Azure Active Directory à FreshGrade</span><span class="sxs-lookup"><span data-stu-id="2bc42-103">Tutorial: Azure Active Directory integration with FreshGrade</span></span>

<span data-ttu-id="2bc42-104">Dans ce didacticiel, vous apprendrez comment toointegrate FreshGrade avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2bc42-104">In this tutorial, you learn how toointegrate FreshGrade with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2bc42-105">Intégration FreshGrade à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2bc42-105">Integrating FreshGrade with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2bc42-106">Vous pouvez contrôler dans Azure AD qui a accès tooFreshGrade</span><span class="sxs-lookup"><span data-stu-id="2bc42-106">You can control in Azure AD who has access tooFreshGrade</span></span>
- <span data-ttu-id="2bc42-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooFreshGrade (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bc42-107">You can enable your users tooautomatically get signed-on tooFreshGrade (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2bc42-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="2bc42-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="2bc42-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2bc42-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bc42-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2bc42-110">Prerequisites</span></span>

<span data-ttu-id="2bc42-111">tooconfigure intégration d’Azure AD avec FreshGrade, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2bc42-111">tooconfigure Azure AD integration with FreshGrade, you need hello following items:</span></span>

- <span data-ttu-id="2bc42-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bc42-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2bc42-113">Un abonnement FreshGrade pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2bc42-113">A FreshGrade single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2bc42-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2bc42-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2bc42-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="2bc42-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2bc42-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2bc42-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="2bc42-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2bc42-117">If you don't have an Azure AD trial environment, you can get a one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2bc42-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2bc42-118">Scenario description</span></span>
<span data-ttu-id="2bc42-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2bc42-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2bc42-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="2bc42-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2bc42-121">Ajout de FreshGrade à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2bc42-121">Adding FreshGrade from hello gallery</span></span>
2. <span data-ttu-id="2bc42-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bc42-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-freshgrade-from-hello-gallery"></a><span data-ttu-id="2bc42-123">Ajout de FreshGrade à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2bc42-123">Adding FreshGrade from hello gallery</span></span>
<span data-ttu-id="2bc42-124">intégration de hello tooconfigure de FreshGrade dans Azure AD, vous devez tooadd FreshGrade à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2bc42-124">tooconfigure hello integration of FreshGrade into Azure AD, you need tooadd FreshGrade from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2bc42-125">**tooadd FreshGrade à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2bc42-125">**tooadd FreshGrade from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2bc42-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="2bc42-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2bc42-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2bc42-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2bc42-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2bc42-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2bc42-133">Dans la zone de recherche de hello, tapez **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-133">In hello search box, type **FreshGrade**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_search.png)

5. <span data-ttu-id="2bc42-135">Dans le volet de résultats hello, sélectionnez **FreshGrade**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2bc42-135">In hello results panel, select **FreshGrade**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2bc42-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bc42-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2bc42-138">Dans cette section, vous configurez et testez l’authentification unique Azure AD avec FreshGrade avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2bc42-138">In this section, you configure and test Azure AD single sign-on with FreshGrade based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2bc42-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans FreshGrade est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2bc42-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in FreshGrade is tooa user in Azure AD.</span></span> <span data-ttu-id="2bc42-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans FreshGrade doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="2bc42-140">In other words, a link relationship between an Azure AD user and hello related user in FreshGrade needs toobe established.</span></span>

<span data-ttu-id="2bc42-141">Dans FreshGrade, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="2bc42-141">In FreshGrade, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="2bc42-142">tooconfigure et test Azure AD l’authentification unique avec FreshGrade, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="2bc42-142">tooconfigure and test Azure AD single sign-on with FreshGrade, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2bc42-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2bc42-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2bc42-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2bc42-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2bc42-145">**[Création d’un utilisateur de test FreshGrade](#creating-a-freshgrade-test-user)**  -toohave un équivalent de Britta Simon dans FreshGrade est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2bc42-145">**[Creating a FreshGrade test user](#creating-a-freshgrade-test-user)** - toohave a counterpart of Britta Simon in FreshGrade that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="2bc42-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2bc42-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2bc42-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="2bc42-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2bc42-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bc42-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2bc42-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre application FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="2bc42-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your FreshGrade application.</span></span>

<span data-ttu-id="2bc42-150">**tooconfigure Azure AD single sign-on avec FreshGrade, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2bc42-150">**tooconfigure Azure AD single sign-on with FreshGrade, perform hello following steps:**</span></span>

1. <span data-ttu-id="2bc42-151">Bonjour portail Azure, sur hello **FreshGrade** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-151">In hello Azure portal, on hello **FreshGrade** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2bc42-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2bc42-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_samlbase.png)

3. <span data-ttu-id="2bc42-155">Sur hello **FreshGrade domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2bc42-155">On hello **FreshGrade Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_url.png)

    <span data-ttu-id="2bc42-157">a.</span><span class="sxs-lookup"><span data-stu-id="2bc42-157">a.</span></span> <span data-ttu-id="2bc42-158">Bonjour **URL de connexion** modèles de zone de texte, tapez une URL à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="2bc42-158">In hello **Sign-on URL** textbox, type a URL using hello following patterns:</span></span> 
      | |
      |--|
      | `https://<subdomain>.freshgrade.com/login` |    
      | `https://<subdomain>.onboarding.freshgrade.com/login` |

    <span data-ttu-id="2bc42-159">b.</span><span class="sxs-lookup"><span data-stu-id="2bc42-159">b.</span></span> <span data-ttu-id="2bc42-160">Bonjour **identificateur** modèles de zone de texte, tapez une URL à l’aide de hello suivant :</span><span class="sxs-lookup"><span data-stu-id="2bc42-160">In hello **Identifier** textbox, type a URL using hello following patterns:</span></span> 
      | |
      |--|
      | `https://login.onboarding.freshgrade.com:443/saml/metadata/alias/<instancename>` |      
      | `https://login.freshgrade.com:443/saml/metadata/alias/<instancename>` |

    > [!NOTE] 
    > <span data-ttu-id="2bc42-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="2bc42-161">These values are not real.</span></span> <span data-ttu-id="2bc42-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="2bc42-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="2bc42-163">Contact [équipe de support Client de FreshGrade](mailTo:support@freshgrade.com) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="2bc42-163">Contact [FreshGrade Client support team](mailTo:support@freshgrade.com) tooget these values.</span></span> 
 


4. <span data-ttu-id="2bc42-164">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2bc42-164">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_certificate.png) 

5. <span data-ttu-id="2bc42-166">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="2bc42-166">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="2bc42-168">Sur hello **FreshGrade Configuration** , cliquez sur **FreshGrade de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="2bc42-168">On hello **FreshGrade Configuration** section, click **Configure FreshGrade** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="2bc42-169">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="2bc42-169">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_configure.png) 

7. <span data-ttu-id="2bc42-171">toogenerate hello **métadonnées** url, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2bc42-171">toogenerate hello **Metadata** url, perform hello following steps:</span></span>

    <span data-ttu-id="2bc42-172">a.</span><span class="sxs-lookup"><span data-stu-id="2bc42-172">a.</span></span> <span data-ttu-id="2bc42-173">Cliquez sur **Inscriptions des applications**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-173">Click **App registrations**.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appregistrations.png)
   
    <span data-ttu-id="2bc42-175">b.</span><span class="sxs-lookup"><span data-stu-id="2bc42-175">b.</span></span> <span data-ttu-id="2bc42-176">Cliquez sur **points de terminaison** tooopen **points de terminaison** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2bc42-176">Click **Endpoints** tooopen **Endpoints** dialog box.</span></span>  
    
    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpointicon.png)

    <span data-ttu-id="2bc42-178">c.</span><span class="sxs-lookup"><span data-stu-id="2bc42-178">c.</span></span> <span data-ttu-id="2bc42-179">Cliquez sur hello copie bouton toocopy **DOCUMENT de métadonnées de fédération** url et collez-le dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="2bc42-179">Click hello copy button toocopy **FEDERATION METADATA DOCUMENT** url and paste it into notepad.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_endpoint.png)
     
    <span data-ttu-id="2bc42-181">d.</span><span class="sxs-lookup"><span data-stu-id="2bc42-181">d.</span></span> <span data-ttu-id="2bc42-182">Maintenant accédez toohello page de propriétés de **FreshGrade** et copie Bonjour **Id d’Application** à l’aide de **copie** bouton et collez-le dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="2bc42-182">Now go toohello property page of **FreshGrade** and copy hello **Application Id** using **Copy** button and paste it into notepad.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_appid.png)

    <span data-ttu-id="2bc42-184">e.</span><span class="sxs-lookup"><span data-stu-id="2bc42-184">e.</span></span> <span data-ttu-id="2bc42-185">Générer hello **URL de métadonnées** hello suivant le modèle à l’aide de :`<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span><span class="sxs-lookup"><span data-stu-id="2bc42-185">Generate hello **Metadata URL** using hello following pattern: `<FEDERATION METADATA DOCUMENT url>?appid=<application id>`</span></span>

8. <span data-ttu-id="2bc42-186">tooconfigure l’authentification unique sur **FreshGrade** côté, vous devez toosend hello **URL de métadonnées** et **SAML Sign-On URL du Service unique** trop[FreshGrade l’équipe de support](mailTo:support@freshgrade.com).</span><span class="sxs-lookup"><span data-stu-id="2bc42-186">tooconfigure single sign-on on **FreshGrade** side, you need toosend hello **Metadata URL** and **SAML Single Sign-On Service URL** too[FreshGrade support team](mailTo:support@freshgrade.com).</span></span> <span data-ttu-id="2bc42-187">Ils définir ce hello toohave de paramètre connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="2bc42-187">They set this setting toohave hello SAML SSO connection set properly on both sides.</span></span>

> [!TIP]
> <span data-ttu-id="2bc42-188">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="2bc42-188">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="2bc42-189">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="2bc42-189">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="2bc42-190">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="2bc42-190">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2bc42-191">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bc42-191">Creating an Azure AD test user</span></span>
<span data-ttu-id="2bc42-192">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="2bc42-192">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2bc42-194">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2bc42-194">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2bc42-195">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="2bc42-195">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2bc42-197">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-197">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2bc42-199">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="2bc42-199">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2bc42-201">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2bc42-201">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-freshgrade-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2bc42-203">a.</span><span class="sxs-lookup"><span data-stu-id="2bc42-203">a.</span></span> <span data-ttu-id="2bc42-204">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-204">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2bc42-205">b.</span><span class="sxs-lookup"><span data-stu-id="2bc42-205">b.</span></span> <span data-ttu-id="2bc42-206">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2bc42-206">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2bc42-207">c.</span><span class="sxs-lookup"><span data-stu-id="2bc42-207">c.</span></span> <span data-ttu-id="2bc42-208">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-208">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2bc42-209">d.</span><span class="sxs-lookup"><span data-stu-id="2bc42-209">d.</span></span> <span data-ttu-id="2bc42-210">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-210">Click **Create**.</span></span>
 
### <a name="creating-a-freshgrade-test-user"></a><span data-ttu-id="2bc42-211">Création d’un utilisateur de test FreshGrade</span><span class="sxs-lookup"><span data-stu-id="2bc42-211">Creating a FreshGrade test user</span></span>

<span data-ttu-id="2bc42-212">Dans cette section, vous créez un utilisateur appelé Britta Simon dans FreshGrade.</span><span class="sxs-lookup"><span data-stu-id="2bc42-212">In this section, you create a user called Britta Simon in FreshGrade.</span></span> <span data-ttu-id="2bc42-213">Collaborez avec [équipe de support FreshGrade](mailTo:support@freshgrade.com) tooadd les utilisateurs de hello dans la plateforme de FreshGrade hello.</span><span class="sxs-lookup"><span data-stu-id="2bc42-213">Please work with [FreshGrade support team](mailTo:support@freshgrade.com) tooadd hello users in hello FreshGrade platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2bc42-214">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2bc42-214">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2bc42-215">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooFreshGrade.</span><span class="sxs-lookup"><span data-stu-id="2bc42-215">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooFreshGrade.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2bc42-217">**tooassign Britta Simon tooFreshGrade, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2bc42-217">**tooassign Britta Simon tooFreshGrade, perform hello following steps:**</span></span>

1. <span data-ttu-id="2bc42-218">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-218">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2bc42-220">Dans la liste des applications hello, sélectionnez **FreshGrade**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-220">In hello applications list, select **FreshGrade**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-freshgrade-tutorial/tutorial_freshgrade_app.png) 

3. <span data-ttu-id="2bc42-222">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-222">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2bc42-224">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-224">Click **Add** button.</span></span> <span data-ttu-id="2bc42-225">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-225">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2bc42-227">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="2bc42-227">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2bc42-228">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-228">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2bc42-229">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2bc42-229">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2bc42-230">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2bc42-230">Testing single sign-on</span></span>

<span data-ttu-id="2bc42-231">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="2bc42-231">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2bc42-232">Lorsque vous cliquez sur mosaïque FreshGrade hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour FreshGrade application.</span><span class="sxs-lookup"><span data-stu-id="2bc42-232">When you click hello FreshGrade tile in hello Access Panel, you should get automatically signed-on tooyour FreshGrade application.</span></span>
<span data-ttu-id="2bc42-233">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="2bc42-233">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2bc42-234">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2bc42-234">Additional resources</span></span>

* [<span data-ttu-id="2bc42-235">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2bc42-235">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2bc42-236">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2bc42-236">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-freshgrade-tutorial/tutorial_general_203.png

