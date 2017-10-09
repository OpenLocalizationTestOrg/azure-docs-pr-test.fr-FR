---
title: "Didacticiel : Intégration d’Azure Active Directory à ServiceChannel | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de ServiceChannel."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c3546eab-96b5-489b-a309-b895eb428053
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/3/2017
ms.author: jeedes
ms.openlocfilehash: 956371a1e99dcba4137c271ecfe8a62b9ec64a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-servicechannel"></a><span data-ttu-id="0a99e-103">Didacticiel : Intégration d’Azure Active Directory à ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="0a99e-103">Tutorial: Azure Active Directory integration with ServiceChannel</span></span>

<span data-ttu-id="0a99e-104">Dans ce didacticiel, vous apprendrez comment toointegrate ServiceChannel avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0a99e-104">In this tutorial, you learn how toointegrate ServiceChannel with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="0a99e-105">Intégration ServiceChannel à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="0a99e-105">Integrating ServiceChannel with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="0a99e-106">Vous pouvez contrôler dans Azure AD qui a accès tooServiceChannel</span><span class="sxs-lookup"><span data-stu-id="0a99e-106">You can control in Azure AD who has access tooServiceChannel</span></span>
- <span data-ttu-id="0a99e-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooServiceChannel (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a99e-107">You can enable your users tooautomatically get signed-on tooServiceChannel (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="0a99e-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="0a99e-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="0a99e-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0a99e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a99e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0a99e-110">Prerequisites</span></span>

<span data-ttu-id="0a99e-111">tooconfigure intégration d’Azure AD avec ServiceChannel, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0a99e-111">tooconfigure Azure AD integration with ServiceChannel, you need hello following items:</span></span>

- <span data-ttu-id="0a99e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a99e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="0a99e-113">Un abonnement ServiceChannel pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="0a99e-113">A ServiceChannel single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="0a99e-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="0a99e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="0a99e-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="0a99e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="0a99e-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0a99e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="0a99e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0a99e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="0a99e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="0a99e-118">Scenario description</span></span>
<span data-ttu-id="0a99e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="0a99e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="0a99e-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="0a99e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="0a99e-121">Ajout de ServiceChannel à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="0a99e-121">Adding ServiceChannel from hello gallery</span></span>
2. <span data-ttu-id="0a99e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a99e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-servicechannel-from-hello-gallery"></a><span data-ttu-id="0a99e-123">Ajout de ServiceChannel à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="0a99e-123">Adding ServiceChannel from hello gallery</span></span>
<span data-ttu-id="0a99e-124">intégration de hello tooconfigure de ServiceChannel dans Azure AD, vous devez tooadd ServiceChannel à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="0a99e-124">tooconfigure hello integration of ServiceChannel into Azure AD, you need tooadd ServiceChannel from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="0a99e-125">**tooadd ServiceChannel à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0a99e-125">**tooadd ServiceChannel from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a99e-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="0a99e-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="0a99e-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="0a99e-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="0a99e-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="0a99e-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="0a99e-133">Dans la zone de recherche de hello, tapez **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-133">In hello search box, type **ServiceChannel**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_000.png)

5. <span data-ttu-id="0a99e-135">Dans le volet de résultats hello, sélectionnez **ServiceChannel**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="0a99e-135">In hello results panel, select **ServiceChannel**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_2.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="0a99e-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a99e-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="0a99e-138">Dans cette section, vous configurez et vous testez l’authentification unique Azure AD avec ServiceChannel avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="0a99e-138">In this section, you configure and test Azure AD single sign-on with ServiceChannel based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="0a99e-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans ServiceChannel est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0a99e-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in ServiceChannel is tooa user in Azure AD.</span></span> <span data-ttu-id="0a99e-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans ServiceChannel doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="0a99e-140">In other words, a link relationship between an Azure AD user and hello related user in ServiceChannel needs toobe established.</span></span>

<span data-ttu-id="0a99e-141">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="0a99e-141">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in ServiceChannel.</span></span>

<span data-ttu-id="0a99e-142">tooconfigure et test Azure AD l’authentification unique avec ServiceChannel, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="0a99e-142">tooconfigure and test Azure AD single sign-on with ServiceChannel, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="0a99e-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="0a99e-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="0a99e-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a99e-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="0a99e-145">**[Création d’un utilisateur de test ServiceChannel](#creating-a-servicechannel-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a99e-145">**[Creating a ServiceChannel test user](#creating-a-servicechannel-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="0a99e-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0a99e-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="0a99e-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="0a99e-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="0a99e-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a99e-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="0a99e-149">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application de ServiceChannel.</span><span class="sxs-lookup"><span data-stu-id="0a99e-149">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your ServiceChannel application.</span></span>

<span data-ttu-id="0a99e-150">**tooconfigure Azure AD single sign-on avec ServiceChannel, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0a99e-150">**tooconfigure Azure AD single sign-on with ServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a99e-151">Dans le portail de gestion Azure hello, sur hello **ServiceChannel** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-151">In hello Azure Management portal, on hello **ServiceChannel** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="0a99e-153">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="0a99e-153">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_01.png)

3. <span data-ttu-id="0a99e-155">Sur hello **ServiceChannel domaine et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="0a99e-155">On hello **ServiceChannel Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_urls.png)

    <span data-ttu-id="0a99e-157">a.</span><span class="sxs-lookup"><span data-stu-id="0a99e-157">a.</span></span> <span data-ttu-id="0a99e-158">Bonjour **identificateur** valeur hello de type en tant que zone de texte :`http://adfs.<domain>.com/adfs/service/trust`</span><span class="sxs-lookup"><span data-stu-id="0a99e-158">In hello **Identifier** textbox, type hello value as: `http://adfs.<domain>.com/adfs/service/trust`</span></span>

    <span data-ttu-id="0a99e-159">b.</span><span class="sxs-lookup"><span data-stu-id="0a99e-159">b.</span></span> <span data-ttu-id="0a99e-160">Bonjour **URL de réponse** zone de texte, tapez une URL à l’aide de hello modèle :`https://<customer domain>.servicechannel.com/saml/acs`</span><span class="sxs-lookup"><span data-stu-id="0a99e-160">In hello **Reply URL** textbox, type a URL using hello following pattern: `https://<customer domain>.servicechannel.com/saml/acs`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="0a99e-161">Notez qu’il s’agit pas des valeurs réelles hello.</span><span class="sxs-lookup"><span data-stu-id="0a99e-161">Please note that these are not hello real values.</span></span> <span data-ttu-id="0a99e-162">Vous avez tooupdate ces valeurs avec hello URL d’identificateur et de réponse réelle.</span><span class="sxs-lookup"><span data-stu-id="0a99e-162">You have tooupdate these values with hello actual Identifier and Reply URL.</span></span> <span data-ttu-id="0a99e-163">Ici, nous vous suggérons vous toouse hello unique valeur de chaîne Bonjour identificateur.</span><span class="sxs-lookup"><span data-stu-id="0a99e-163">Here we suggest you toouse hello unique value of string in hello Identifier.</span></span> <span data-ttu-id="0a99e-164">Contact [équipe de support ServiceChannel](https://servicechannel.zendesk.com/hc/en-us) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="0a99e-164">Contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us) tooget these values.</span></span>

4. <span data-ttu-id="0a99e-165">Votre application ServiceChannel attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.</span><span class="sxs-lookup"><span data-stu-id="0a99e-165">Your ServiceChannel application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="0a99e-166">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="0a99e-166">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="0a99e-167">**NameIdentifier (identifiant d’utilisateur)** est hello uniquement les revendications obligatoires et la valeur par défaut hello est **user.userprincipalname** mais ServiceChannel attend ce toobe mappée avec **user.mail**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-167">**NameIdentifier(User Identifier)** is hello only mandatory claim and hello default value is **user.userprincipalname** but ServiceChannel expects this toobe mapped with **user.mail**.</span></span> <span data-ttu-id="0a99e-168">Si vous envisagez de l’approvisionnement des utilisateurs tooenable juste à temps, vous devez ajouter hello suivant revendications comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="0a99e-168">If you are planning tooenable Just In Time user provisioning, then you should add hello following claims as shown below.</span></span> <span data-ttu-id="0a99e-169">**Rôle** revendication doit toobe mappé trop**user.assignedroles** qui contient le rôle utilisateur de hello hello.</span><span class="sxs-lookup"><span data-stu-id="0a99e-169">**Role** claim needs toobe mapped too**user.assignedroles** which contains hello role of hello user.</span></span>  

    <span data-ttu-id="0a99e-170">Vous pouvez consulter le guide de ServiceChannel [ici](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) pour obtenir des instructions sur les revendications.</span><span class="sxs-lookup"><span data-stu-id="0a99e-170">You can refer ServiceChannel guide [here](https://servicechannel.zendesk.com/hc/en-us/articles/217514326-Azure-AD-Configuration-Example) for more guidance on claims.</span></span>
    
    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_attribute.png)

    > [!NOTE] 
    > <span data-ttu-id="0a99e-172">Cliquez sur [ici](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow comment tooconfigure **rôle** dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a99e-172">Please click [here](http://www.dushyantgill.com/blog/2014/12/10/roles-based-access-control-in-cloud-applications-using-azure-ad/) tooknow how tooconfigure **Role** in Azure AD</span></span>

5. <span data-ttu-id="0a99e-173">Dans **attributs utilisateur** , cliquez sur **afficher et modifier tous les autres attributs utilisateur** et définir les attributs de hello.</span><span class="sxs-lookup"><span data-stu-id="0a99e-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span>

    | <span data-ttu-id="0a99e-174">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="0a99e-174">Attribute Name</span></span> | <span data-ttu-id="0a99e-175">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="0a99e-175">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="0a99e-176">Rôle</span><span class="sxs-lookup"><span data-stu-id="0a99e-176">Role</span></span>| <span data-ttu-id="0a99e-177">user.assignedroles</span><span class="sxs-lookup"><span data-stu-id="0a99e-177">user.assignedroles</span></span> |

    <span data-ttu-id="0a99e-178">a.</span><span class="sxs-lookup"><span data-stu-id="0a99e-178">a.</span></span> <span data-ttu-id="0a99e-179">Cliquez sur **ajouter un attribut** tooopen hello **ajouter un attribut** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0a99e-179">Click **Add attribute** tooopen hello **Add Attribute** dialog.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial_servicechannel_05.png)
    
    <span data-ttu-id="0a99e-182">b.</span><span class="sxs-lookup"><span data-stu-id="0a99e-182">b.</span></span> <span data-ttu-id="0a99e-183">Bonjour **nom** zone de texte, nom d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="0a99e-183">In hello **Name** textbox, type hello attribute name shown for that row.</span></span>
    
    <span data-ttu-id="0a99e-184">c.</span><span class="sxs-lookup"><span data-stu-id="0a99e-184">c.</span></span> <span data-ttu-id="0a99e-185">À partir de hello **valeur** liste, la valeur d’attribut type hello indiqué pour cette ligne.</span><span class="sxs-lookup"><span data-stu-id="0a99e-185">From hello **Value** list, type hello attribute value shown for that row.</span></span>
    
    <span data-ttu-id="0a99e-186">d.</span><span class="sxs-lookup"><span data-stu-id="0a99e-186">d.</span></span> <span data-ttu-id="0a99e-187">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-187">Click **Ok**</span></span>
    
6. <span data-ttu-id="0a99e-188">Sur hello **le certificat de signature SAML** , cliquez sur **certificat (Base64)** , puis enregistrez le fichier de certificat hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0a99e-188">On hello **SAML Signing Certificate** section, click **Certificate (Base64)** and then save hello certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_05.png) 

7. <span data-ttu-id="0a99e-190">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-190">Click **Save**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="0a99e-192">Sur hello **ServiceChannel Configuration** , cliquez sur **ServiceChannel de configurer** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="0a99e-192">On hello **ServiceChannel Configuration** section, click **Configure ServiceChannel** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="0a99e-193">Veuillez noter hello **ID d’entité SAML** de hello **aide-mémoire** section.</span><span class="sxs-lookup"><span data-stu-id="0a99e-193">Please note hello **SAML Enitity ID** from hello **Quick Reference** section.</span></span>

9. <span data-ttu-id="0a99e-194">tooconfigure l’authentification unique sur **ServiceChannel** côté, vous devez hello toosend téléchargé **certificat (Base64)** et **ID d’entité SAML** trop[ Équipe de support ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="0a99e-194">tooconfigure single sign-on on **ServiceChannel** side, you need toosend hello downloaded **certificate (Base64)** and **SAML Entity ID** too[ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us).</span></span> <span data-ttu-id="0a99e-195">Ils seront configurer Bonjour de toohave commande connexion SSO SAML correctement des deux côtés.</span><span class="sxs-lookup"><span data-stu-id="0a99e-195">They will set this up in order toohave hello SAML SSO connection set properly on both sides.</span></span>

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="0a99e-196">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a99e-196">Creating an Azure AD test user</span></span>
<span data-ttu-id="0a99e-197">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="0a99e-197">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="0a99e-199">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0a99e-199">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a99e-200">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="0a99e-200">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="0a99e-202">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="0a99e-202">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="0a99e-204">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="0a99e-204">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="0a99e-206">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="0a99e-206">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-servicechannel-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="0a99e-208">a.</span><span class="sxs-lookup"><span data-stu-id="0a99e-208">a.</span></span> <span data-ttu-id="0a99e-209">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-209">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="0a99e-210">b.</span><span class="sxs-lookup"><span data-stu-id="0a99e-210">b.</span></span> <span data-ttu-id="0a99e-211">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="0a99e-211">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="0a99e-212">c.</span><span class="sxs-lookup"><span data-stu-id="0a99e-212">c.</span></span> <span data-ttu-id="0a99e-213">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-213">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="0a99e-214">d.</span><span class="sxs-lookup"><span data-stu-id="0a99e-214">d.</span></span> <span data-ttu-id="0a99e-215">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-215">Click **Create**.</span></span> 

### <a name="creating-a-servicechannel-test-user"></a><span data-ttu-id="0a99e-216">Création d’un utilisateur de test ServiceChannel</span><span class="sxs-lookup"><span data-stu-id="0a99e-216">Creating a ServiceChannel test user</span></span>

<span data-ttu-id="0a99e-217">Application prend en charge juste configuration en temps utilisateur et une fois que les utilisateurs de l’authentification seront créées automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="0a99e-217">Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="0a99e-218">Pour l’approvisionnement de l’utilisateur complet, contactez l’[équipe de support technique de ServiceChannel](https://servicechannel.zendesk.com/hc/en-us).</span><span class="sxs-lookup"><span data-stu-id="0a99e-218">For full user provisioning, please contact [ServiceChannel support team](https://servicechannel.zendesk.com/hc/en-us)</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="0a99e-219">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="0a99e-219">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="0a99e-220">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant tooServiceChannel de son accès.</span><span class="sxs-lookup"><span data-stu-id="0a99e-220">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooServiceChannel.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="0a99e-222">**tooassign Britta Simon tooServiceChannel, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="0a99e-222">**tooassign Britta Simon tooServiceChannel, perform hello following steps:**</span></span>

1. <span data-ttu-id="0a99e-223">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-223">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="0a99e-225">Dans la liste des applications hello, sélectionnez **ServiceChannel**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-225">In hello applications list, select **ServiceChannel**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-servicechannel-tutorial/tutorial-servicechannel_app01.png) 

3. <span data-ttu-id="0a99e-227">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-227">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="0a99e-229">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-229">Click **Add** button.</span></span> <span data-ttu-id="0a99e-230">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-230">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="0a99e-232">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="0a99e-232">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="0a99e-233">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-233">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="0a99e-234">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="0a99e-234">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="0a99e-235">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="0a99e-235">Testing single sign-on</span></span>

<span data-ttu-id="0a99e-236">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="0a99e-236">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="0a99e-237">Lorsque vous cliquez sur mosaïque ServiceChannel hello hello volet d’accès, vous devez obtenir automatiquement signé sur tooyour ServiceChannel application.</span><span class="sxs-lookup"><span data-stu-id="0a99e-237">When you click hello ServiceChannel tile in hello Access Panel, you should get automatically signed-on tooyour ServiceChannel application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0a99e-238">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="0a99e-238">Additional resources</span></span>

* [<span data-ttu-id="0a99e-239">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0a99e-239">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="0a99e-240">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="0a99e-240">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-servicechannel-tutorial/tutorial_general_203.png