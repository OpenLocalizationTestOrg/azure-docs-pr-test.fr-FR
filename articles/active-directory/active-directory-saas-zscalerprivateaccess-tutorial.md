---
title: "Didacticiel : Intégration d’Azure Active Directory à Zscaler Private Access (ZPA) | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’accès privé de Zscaler (ZPA)."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 83711115-1c4f-4dd7-907b-3da24b37c89e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jeedes
ms.openlocfilehash: 0370cff60c8ac15bd1919acccc924da1e50dc45b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-private-access-zpa"></a><span data-ttu-id="dfd50-103">Didacticiel : Intégration d’Azure Active Directory à Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="dfd50-103">Tutorial: Azure Active Directory integration with Zscaler Private Access (ZPA)</span></span>

<span data-ttu-id="dfd50-104">Dans ce didacticiel, vous apprendrez comment toointegrate Zscaler privé accès (ZPA) avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dfd50-104">In this tutorial, you learn how toointegrate Zscaler Private Access (ZPA) with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="dfd50-105">Intégration d’accès privé de Zscaler (ZPA) à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="dfd50-105">Integrating Zscaler Private Access (ZPA) with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="dfd50-106">Vous pouvez contrôler dans Azure AD qui a accès tooZscaler accès privé (ZPA)</span><span class="sxs-lookup"><span data-stu-id="dfd50-106">You can control in Azure AD who has access tooZscaler Private Access (ZPA)</span></span>
- <span data-ttu-id="dfd50-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooZscaler accès privé (ZPA) (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfd50-107">You can enable your users tooautomatically get signed-on tooZscaler Private Access (ZPA) (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="dfd50-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="dfd50-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="dfd50-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="dfd50-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dfd50-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="dfd50-110">Prerequisites</span></span>

<span data-ttu-id="dfd50-111">tooconfigure intégration d’Azure AD avec Zscaler privé accès (ZPA), vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="dfd50-111">tooconfigure Azure AD integration with Zscaler Private Access (ZPA), you need hello following items:</span></span>

- <span data-ttu-id="dfd50-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfd50-112">An Azure AD subscription</span></span>
- <span data-ttu-id="dfd50-113">Un abonnement Zscaler Private Access (ZPA) activé via l’authentification unique (SSO)</span><span class="sxs-lookup"><span data-stu-id="dfd50-113">A Zscaler Private Access (ZPA) single-sign on enabled subscription</span></span>


> [!NOTE]
> <span data-ttu-id="dfd50-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="dfd50-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>


<span data-ttu-id="dfd50-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="dfd50-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="dfd50-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dfd50-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="dfd50-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dfd50-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>


## <a name="scenario-description"></a><span data-ttu-id="dfd50-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="dfd50-118">Scenario description</span></span>
<span data-ttu-id="dfd50-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="dfd50-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="dfd50-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="dfd50-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="dfd50-121">Ajout d’accès privé de Zscaler (ZPA) à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dfd50-121">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
2. <span data-ttu-id="dfd50-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfd50-122">Configuring and testing Azure AD single sign-on</span></span>


## <a name="adding-zscaler-private-access-zpa-from-hello-gallery"></a><span data-ttu-id="dfd50-123">Ajout d’accès privé de Zscaler (ZPA) à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="dfd50-123">Adding Zscaler Private Access (ZPA) from hello gallery</span></span>
<span data-ttu-id="dfd50-124">intégration de hello tooconfigure de Zscaler privé accès (ZPA) dans Azure AD, vous devez tooadd accès privé de Zscaler (ZPA) à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="dfd50-124">tooconfigure hello integration of Zscaler Private Access (ZPA) into Azure AD, you need tooadd Zscaler Private Access (ZPA) from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="dfd50-125">**tooadd Zscaler privé accès (ZPA) à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dfd50-125">**tooadd Zscaler Private Access (ZPA) from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfd50-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="dfd50-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="dfd50-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="dfd50-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="dfd50-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="dfd50-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="dfd50-133">Dans la zone de recherche de hello, tapez **accès privé de Zscaler (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-133">In hello search box, type **Zscaler Private Access (ZPA)**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_001.png)

5. <span data-ttu-id="dfd50-135">Dans le volet de résultats hello, sélectionnez **accès privé de Zscaler (ZPA)**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="dfd50-135">In hello results panel, select **Zscaler Private Access (ZPA)**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_0001.png)


##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="dfd50-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfd50-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="dfd50-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec Zscaler Private Access (ZPA) avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="dfd50-138">In this section, you configure and test Azure AD single sign-on with Zscaler Private Access (ZPA) based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="dfd50-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans Zscaler privé accès (ZPA) est tooa dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dfd50-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in Zscaler Private Access (ZPA) is tooa user in Azure AD.</span></span> <span data-ttu-id="dfd50-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans Zscaler privé accès (ZPA) doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="dfd50-140">In other words, a link relationship between an Azure AD user and hello related user in Zscaler Private Access (ZPA) needs toobe established.</span></span>

<span data-ttu-id="dfd50-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans Zscaler privé accès (ZPA).</span><span class="sxs-lookup"><span data-stu-id="dfd50-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in Zscaler Private Access (ZPA).</span></span>

<span data-ttu-id="dfd50-142">tooconfigure et test Azure AD l’authentification unique avec Zscaler privé accès (ZPA), vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="dfd50-142">tooconfigure and test Azure AD single sign-on with Zscaler Private Access (ZPA), you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="dfd50-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="dfd50-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="dfd50-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dfd50-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="dfd50-145">**[Création d’un utilisateur de test de Zscaler privé accès (ZPA)](#creating-a-zscaler-private-access-(zpa)-test-user)**  -toohave de Britta Simon dans Zscaler privé accès (ZPA) qui est la représentation sous forme de toohello lié Azure AD de sa contrepartie.</span><span class="sxs-lookup"><span data-stu-id="dfd50-145">**[Creating a Zscaler Private Access (ZPA) test user](#creating-a-zscaler-private-access-(zpa)-test-user)** - toohave a counterpart of Britta Simon in Zscaler Private Access (ZPA) that is linked toohello Azure AD representation of her.</span></span>
4. <span data-ttu-id="dfd50-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dfd50-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="dfd50-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="dfd50-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="dfd50-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfd50-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="dfd50-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application Zscaler privé accès (ZPA).</span><span class="sxs-lookup"><span data-stu-id="dfd50-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your Zscaler Private Access (ZPA) application.</span></span>

<span data-ttu-id="dfd50-150">**tooconfigure Azure AD l’authentification unique avec Zscaler privé accès (ZPA), exécutez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dfd50-150">**tooconfigure Azure AD single sign-on with Zscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="dfd50-151">Dans le portail de gestion Azure hello, sur hello **accès privé de Zscaler (ZPA)** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-151">In hello Azure Management portal, on hello **Zscaler Private Access (ZPA)** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="dfd50-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="dfd50-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_300.png)
    
3. <span data-ttu-id="dfd50-155">Sur hello **Zscaler privé accès (ZPA) domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dfd50-155">On hello **Zscaler Private Access (ZPA) Domain and URLs** section, perform hello following steps:</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_01.png)

    <span data-ttu-id="dfd50-157">a.</span><span class="sxs-lookup"><span data-stu-id="dfd50-157">a.</span></span> <span data-ttu-id="dfd50-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span><span class="sxs-lookup"><span data-stu-id="dfd50-158">In hello **Sign On URL** textbox, type a URL using hello following pattern: `https://samlsp.private.zscaler.com/auth/login?domain=<your-domain-name>`</span></span>

    <span data-ttu-id="dfd50-159">b.</span><span class="sxs-lookup"><span data-stu-id="dfd50-159">b.</span></span> <span data-ttu-id="dfd50-160">Bonjour **identificateur** zone de texte, type :`https://samlsp.private.zscaler.com/auth/metadata`</span><span class="sxs-lookup"><span data-stu-id="dfd50-160">In hello **Identifier** textbox, type: `https://samlsp.private.zscaler.com/auth/metadata`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="dfd50-161">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="dfd50-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="dfd50-162">Vous avez tooupdate ces valeurs avec hello réel connectent URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="dfd50-162">You have tooupdate these values with hello actual Sign On URL and Identifier.</span></span> <span data-ttu-id="dfd50-163">Ici, nous vous suggérons vous toouse hello valeur unique de l’URL dans hello identificateur.</span><span class="sxs-lookup"><span data-stu-id="dfd50-163">Here we suggest you toouse hello unique value of URL in hello Identifier.</span></span> <span data-ttu-id="dfd50-164">Contact [équipe de support technique Zscaler privé accès (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="dfd50-164">Contact [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooget these values.</span></span>

4. <span data-ttu-id="dfd50-165">Sur hello **le certificat de signature SAML** , cliquez sur **créer un nouveau certificat**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-165">On hello **SAML Signing Certificate** section, click **Create new certificate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_400.png)   

5. <span data-ttu-id="dfd50-167">Sur hello **créer un nouveau certificat** boîte de dialogue, cliquez sur icône du calendrier hello et sélectionnez un **date d’expiration**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-167">On hello **Create New Certificate** dialog, click hello calendar icon and select an **expiry date**.</span></span> <span data-ttu-id="dfd50-168">Ensuite, cliquez sur le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-168">Then click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_500.png)

6. <span data-ttu-id="dfd50-170">Sur hello **le certificat de signature SAML** section, sélectionnez **activer le nouveau certificat** et cliquez sur **enregistrer** bouton.</span><span class="sxs-lookup"><span data-stu-id="dfd50-170">On hello **SAML Signing Certificate** section, select **Make new certificate active** and click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_02.png)

7. <span data-ttu-id="dfd50-172">Dans la fenêtre contextuelle de hello **le certificat de substitution** fenêtre, cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-172">On hello pop-up **Rollover certificate** window, click **OK**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_600.png)

8. <span data-ttu-id="dfd50-174">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="dfd50-174">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_03.png) 

9. <span data-ttu-id="dfd50-176">Dans une autre fenêtre de navigateur web, connectez-vous à votre site d’entreprise Zscaler Private Access (ZPA) en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="dfd50-176">In a different web browser window, log into your Zscaler Private Access (ZPA) company site as an administrator.</span></span>

10. <span data-ttu-id="dfd50-177">Accédez trop**administrateur** puis cliquez sur **Idp Configuration**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-177">Navigate too**Administrator** and then click **Idp Configuration**.</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_04.png)

11. <span data-ttu-id="dfd50-179">Bonjour **Idp Configuration** , cliquez sur **ajouter une nouvelle Configuration de fournisseurs d’identité**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-179">In hello **Idp Configuration** section, click **Add New IDP Configuration**.</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_05.png)

12. <span data-ttu-id="dfd50-181">Bonjour **nouvelle Configuration IDP** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dfd50-181">In hello **New IDP Configuration** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique côté application](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_06.png)

    <span data-ttu-id="dfd50-183">a.</span><span class="sxs-lookup"><span data-stu-id="dfd50-183">a.</span></span> <span data-ttu-id="dfd50-184">Cliquez sur **Sélectionner un fichier** et chargez votre fichier de métadonnées téléchargé.</span><span class="sxs-lookup"><span data-stu-id="dfd50-184">Click **Select File** and upload your downloaded metadata file.</span></span>

    <span data-ttu-id="dfd50-185">b.</span><span class="sxs-lookup"><span data-stu-id="dfd50-185">b.</span></span> <span data-ttu-id="dfd50-186">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="dfd50-186">Click **Save** button.</span></span>
    


### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="dfd50-187">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfd50-187">Creating an Azure AD test user</span></span>
<span data-ttu-id="dfd50-188">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="dfd50-188">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="dfd50-190">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dfd50-190">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="dfd50-191">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="dfd50-191">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="dfd50-193">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dfd50-193">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="dfd50-195">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="dfd50-195">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="dfd50-197">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="dfd50-197">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-zscalerprivateaccess-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="dfd50-199">a.</span><span class="sxs-lookup"><span data-stu-id="dfd50-199">a.</span></span> <span data-ttu-id="dfd50-200">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-200">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="dfd50-201">b.</span><span class="sxs-lookup"><span data-stu-id="dfd50-201">b.</span></span> <span data-ttu-id="dfd50-202">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="dfd50-202">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="dfd50-203">c.</span><span class="sxs-lookup"><span data-stu-id="dfd50-203">c.</span></span> <span data-ttu-id="dfd50-204">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-204">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="dfd50-205">d.</span><span class="sxs-lookup"><span data-stu-id="dfd50-205">d.</span></span> <span data-ttu-id="dfd50-206">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-206">Click **Create**.</span></span> 



### <a name="creating-a-zscaler-private-access-zpa-test-user"></a><span data-ttu-id="dfd50-207">Création d’un utilisateur de test Zscaler Private Access (ZPA)</span><span class="sxs-lookup"><span data-stu-id="dfd50-207">Creating a Zscaler Private Access (ZPA) test user</span></span>

<span data-ttu-id="dfd50-208">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans Zscaler Private Access (ZPA).</span><span class="sxs-lookup"><span data-stu-id="dfd50-208">In this section, you create a user called Britta Simon in Zscaler Private Access (ZPA).</span></span> <span data-ttu-id="dfd50-209">Collaborez avec [équipe de support technique Zscaler privé accès (ZPA)](https://help.zscaler.com/zpa-submit-ticket) tooadd les utilisateurs de hello dans la plateforme de Zscaler privé accès (ZPA) hello.</span><span class="sxs-lookup"><span data-stu-id="dfd50-209">Please work with [Zscaler Private Access (ZPA) support team](https://help.zscaler.com/zpa-submit-ticket) tooadd hello users in hello Zscaler Private Access (ZPA) platform.</span></span>


### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="dfd50-210">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="dfd50-210">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="dfd50-211">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooZscaler accès accès privé (ZPA).</span><span class="sxs-lookup"><span data-stu-id="dfd50-211">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooZscaler Private Access (ZPA).</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="dfd50-213">**tooassign Britta Simon tooZscaler accès privé (ZPA), exécutez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="dfd50-213">**tooassign Britta Simon tooZscaler Private Access (ZPA), perform hello following steps:**</span></span>

1. <span data-ttu-id="dfd50-214">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-214">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="dfd50-216">Dans la liste des applications hello, sélectionnez **accès privé de Zscaler (ZPA)**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-216">In hello applications list, select **Zscaler Private Access (ZPA)**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_zscalerprivateaccess_50.png) 

3. <span data-ttu-id="dfd50-218">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-218">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="dfd50-220">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-220">Click **Add** button.</span></span> <span data-ttu-id="dfd50-221">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-221">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="dfd50-223">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="dfd50-223">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="dfd50-224">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-224">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="dfd50-225">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="dfd50-225">Click **Assign** button on **Add Assignment** dialog.</span></span>
    


### <a name="testing-single-sign-on"></a><span data-ttu-id="dfd50-226">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="dfd50-226">Testing single sign-on</span></span>

<span data-ttu-id="dfd50-227">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="dfd50-227">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="dfd50-228">Lorsque vous cliquez sur mosaïque Zscaler privé accès (ZPA) hello hello volet d’accès, vous devez obtenir l’application de Zscaler privé accès (ZPA) tooyour automatiquement signé sur.</span><span class="sxs-lookup"><span data-stu-id="dfd50-228">When you click hello Zscaler Private Access (ZPA) tile in hello Access Panel, you should get automatically signed-on tooyour Zscaler Private Access (ZPA) application.</span></span>


## <a name="additional-resources"></a><span data-ttu-id="dfd50-229">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="dfd50-229">Additional resources</span></span>

* [<span data-ttu-id="dfd50-230">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="dfd50-230">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="dfd50-231">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="dfd50-231">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-zscalerprivateaccess-tutorial/tutorial_general_203.png