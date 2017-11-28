---
title: "Didacticiel : Intégration d’Azure Active Directory à LinkedIn Elevate | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et l’élévation LinkedIn."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 2ad9941b-c574-42c3-bd0f-5d6ec68537ef
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeedes
ms.openlocfilehash: 189bd72c230be7dc0c0b934f94ea01e84af9ad23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-linkedin-elevate"></a><span data-ttu-id="2390e-103">Didacticiel : Intégration d’Azure Active Directory à LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="2390e-103">Tutorial: Azure Active Directory integration with LinkedIn Elevate</span></span>

<span data-ttu-id="2390e-104">Dans ce didacticiel, vous apprendrez comment toointegrate LinkedIn élever avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2390e-104">In this tutorial, you learn how toointegrate LinkedIn Elevate with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="2390e-105">Intégration LinkedIn élever à Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="2390e-105">Integrating LinkedIn Elevate with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="2390e-106">Vous pouvez contrôler dans Azure AD qui a accès tooLinkedIn élever</span><span class="sxs-lookup"><span data-stu-id="2390e-106">You can control in Azure AD who has access tooLinkedIn Elevate</span></span>
- <span data-ttu-id="2390e-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooLinkedIn élever (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="2390e-107">You can enable your users tooautomatically get signed-on tooLinkedIn Elevate (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="2390e-108">Vous pouvez gérer vos comptes dans un emplacement central - portail de gestion Azure hello</span><span class="sxs-lookup"><span data-stu-id="2390e-108">You can manage your accounts in one central location - hello Azure Management portal</span></span>

<span data-ttu-id="2390e-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="2390e-109">If you want tooknow more details about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2390e-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="2390e-110">Prerequisites</span></span>

<span data-ttu-id="2390e-111">tooconfigure intégration d’Azure AD avec LinkedIn élever, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="2390e-111">tooconfigure Azure AD integration with LinkedIn Elevate, you need hello following items:</span></span>

- <span data-ttu-id="2390e-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="2390e-112">An Azure AD subscription</span></span>
- <span data-ttu-id="2390e-113">Un abonnement LinkedIn Elevate pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="2390e-113">A LinkedIn Elevate single-sign on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="2390e-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2390e-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="2390e-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="2390e-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="2390e-116">Vous ne devez pas utiliser votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="2390e-116">You should not use your production environment, unless this is necessary.</span></span>
- <span data-ttu-id="2390e-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois [ici](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2390e-117">If you don't have an Azure AD trial environment, you can get an one-month trial [here](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="2390e-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="2390e-118">Scenario description</span></span>
<span data-ttu-id="2390e-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="2390e-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="2390e-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="2390e-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="2390e-121">Ajout de LinkedIn élever à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2390e-121">Adding LinkedIn Elevate from hello gallery</span></span>
2. <span data-ttu-id="2390e-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2390e-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-linkedin-elevate-from-hello-gallery"></a><span data-ttu-id="2390e-123">Ajout de LinkedIn élever à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="2390e-123">Adding LinkedIn Elevate from hello gallery</span></span>
<span data-ttu-id="2390e-124">tooconfigure hello intégration de LinkedIn élever dans Azure AD, vous devez tooadd LinkedIn élever à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="2390e-124">tooconfigure hello integration of LinkedIn Elevate into Azure AD, you need tooadd LinkedIn Elevate from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="2390e-125">**tooadd LinkedIn élever à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2390e-125">**tooadd LinkedIn Elevate from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="2390e-126">Bonjour  **[portail de gestion Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="2390e-126">In hello **[Azure Management Portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="2390e-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="2390e-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="2390e-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2390e-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="2390e-131">Cliquez sur **ajouter** bouton en haut de hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="2390e-131">Click **Add** button on hello top of hello dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="2390e-133">Dans la zone de recherche de hello, tapez **LinkedIn élever**.</span><span class="sxs-lookup"><span data-stu-id="2390e-133">In hello search box, type **LinkedIn Elevate**.</span></span> <span data-ttu-id="2390e-134">Dans le volet de résultats, cliquez sur **LinkedIn élever** application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="2390e-134">From results panel, click **LinkedIn Elevate** tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_000.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="2390e-136">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2390e-136">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="2390e-137">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec LinkedIn Elevate, avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="2390e-137">In this section, you configure and test Azure AD single sign-on with LinkedIn Elevate based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="2390e-138">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur équivalent hello LinkedIn élever est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2390e-138">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in LinkedIn Elevate is tooa user in Azure AD.</span></span> <span data-ttu-id="2390e-139">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans LinkedIn élever doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="2390e-139">In other words, a link relationship between an Azure AD user and hello related user in LinkedIn Elevate needs toobe established.</span></span>

<span data-ttu-id="2390e-140">Cette relation de lien est établie en assignant la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** dans LinkedIn élever.</span><span class="sxs-lookup"><span data-stu-id="2390e-140">This link relationship is established by assigning hello value of hello **user name** in Azure AD as hello value of hello **Username** in LinkedIn Elevate.</span></span>

<span data-ttu-id="2390e-141">tooconfigure et test Azure AD l’authentification unique avec LinkedIn élever, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="2390e-141">tooconfigure and test Azure AD single sign-on with LinkedIn Elevate, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="2390e-142">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="2390e-142">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="2390e-143">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2390e-143">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="2390e-144">**[Création d’un utilisateur test LinkedIn élever](#creating-a-linkedin-elevate-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2390e-144">**[Creating a LinkedIn Elevate test user](#creating-a-linkedin-elevate-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
4. <span data-ttu-id="2390e-145">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2390e-145">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="2390e-146">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="2390e-146">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="2390e-147">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="2390e-147">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="2390e-148">Dans cette section, vous activez Azure AD l’authentification unique dans le portail de gestion Azure hello et configurez l’authentification unique dans votre application LinkedIn élever.</span><span class="sxs-lookup"><span data-stu-id="2390e-148">In this section, you enable Azure AD single sign-on in hello Azure Management portal and configure single sign-on in your LinkedIn Elevate application.</span></span>

<span data-ttu-id="2390e-149">**tooconfigure Azure AD single sign-on avec LinkedIn élever, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2390e-149">**tooconfigure Azure AD single sign-on with LinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="2390e-150">Dans le portail de gestion Azure hello, sur hello **LinkedIn élever** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="2390e-150">In hello Azure Management portal, on hello **LinkedIn Elevate** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="2390e-152">Sur hello **l’authentification unique** boîte de dialogue, en tant que **Mode** sélectionnez **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="2390e-152">On hello **Single sign-on** dialog, as **Mode** select **SAML-based Sign-on** tooenable single sign on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedin_01.png)

3. <span data-ttu-id="2390e-154">Dans une fenêtre de navigateur web, l’authentification tooyour LinkedIn élever locataire en tant qu’administrateur.</span><span class="sxs-lookup"><span data-stu-id="2390e-154">In a different web browser window, sign-on tooyour LinkedIn Elevate tenant as an administrator.</span></span>

4. <span data-ttu-id="2390e-155">Dans le **Centre des comptes**, cliquez sur **Paramètres globaux** sous **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="2390e-155">In **Account Center**, click **Global Settings** under **Settings**.</span></span> <span data-ttu-id="2390e-156">En outre, sélectionnez **élever - élever un Test AAD** à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="2390e-156">Also, select **Elevate - Elevate AAD Test** from hello dropdown list.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_01.png)

5. <span data-ttu-id="2390e-158">Cliquez sur **ou cliquez ici tooload et copie des champs individuels à partir de l’écran de hello** et copie **Id d’entité** et **Url d’accès ACS (Assertion Consumer)**</span><span class="sxs-lookup"><span data-stu-id="2390e-158">Click on **OR Click Here tooload and copy individual fields from hello form** and copy **Entity Id** and **Assertion Consumer Access (ACS) Url**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_03.png)

6. <span data-ttu-id="2390e-160">Sur le portail Azure, sous **URL et le domaine d’élever LinkedIn**, effectuer hello comme suit si vous souhaitez que l’authentification unique de tooconfigure dans **initialisée par IdP** mode</span><span class="sxs-lookup"><span data-stu-id="2390e-160">On Azure Portal, under **LinkedIn Elevate Domain and URLs**, perform hello following steps if you want tooconfigure SSO in **IdP Initiated** mode</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_01.png)

    <span data-ttu-id="2390e-162">a.</span><span class="sxs-lookup"><span data-stu-id="2390e-162">a.</span></span> <span data-ttu-id="2390e-163">Bonjour **identificateur** zone de texte, entrez hello **ID d’entité** copiés à partir du portail de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="2390e-163">In hello **Identifier** textbox, enter hello **Entity ID** copied from LinkedIn Portal</span></span> 

    <span data-ttu-id="2390e-164">b.</span><span class="sxs-lookup"><span data-stu-id="2390e-164">b.</span></span> <span data-ttu-id="2390e-165">Bonjour **URL de réponse** zone de texte, entrez hello **Url d’accès ACS (Assertion Consumer)** copiés à partir du portail de LinkedIn</span><span class="sxs-lookup"><span data-stu-id="2390e-165">In hello **Reply URL** textbox, enter hello **Assertion Consumer Access (ACS) Url** copied from LinkedIn Portal</span></span>

7. <span data-ttu-id="2390e-166">Si vous souhaitez que l’authentification unique de tooconfigure dans **initiée par SP**, puis cliquez sur option Afficher les URL avancées du paramètre dans la section de configuration hello et configurer l’authentification hello URL avec hello modèle :</span><span class="sxs-lookup"><span data-stu-id="2390e-166">If you want tooconfigure SSO in **SP Initiated**, then click Show Advanced URL setting option in hello configuration section and configure hello sign on URL with hello following pattern:</span></span>

    `https://www.linkedin.com/checkpoint/enterprise/login/<AccountId>?application=elevate&applicationInstanceId=<InstanceId>` 
    
    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_signon_02.png) 
    
8. <span data-ttu-id="2390e-168">Votre application LinkedIn élever attend les assertions SAML hello dans un format spécifique, ce qui nécessite vous tooadd attribut personnalisé tooyour SAML attributs du jeton configuration des mappages.</span><span class="sxs-lookup"><span data-stu-id="2390e-168">Your LinkedIn Elevate application expects hello SAML assertions in a specific format, which requires you tooadd custom attribute mappings tooyour SAML token attributes configuration.</span></span> <span data-ttu-id="2390e-169">Hello suivant capture d’écran montre un exemple de cela.</span><span class="sxs-lookup"><span data-stu-id="2390e-169">hello following screenshot shows an example for this.</span></span> <span data-ttu-id="2390e-170">Hello la valeur par défaut de **identificateur de l’utilisateur** est **user.userprincipalname** mais LinkedIn élever attend ce toobe mappée avec une adresse de messagerie de l’utilisateur hello.</span><span class="sxs-lookup"><span data-stu-id="2390e-170">hello default value of **User Identifier** is **user.userprincipalname** but LinkedIn Elevate expects this toobe mapped with hello user's email address.</span></span> <span data-ttu-id="2390e-171">Pour cela, vous pouvez utiliser **user.mail** d’attribut à partir de la liste de hello ou utiliser la valeur d’attribut approprié hello en fonction de la configuration de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="2390e-171">For that you can use **user.mail** attribute from hello list or use hello appropriate attribute value based on your organization configuration.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/updateusermail.png)

9. <span data-ttu-id="2390e-173">Dans **attributs utilisateur** , cliquez sur **afficher et modifier tous les autres attributs utilisateur** et définir les attributs de hello.</span><span class="sxs-lookup"><span data-stu-id="2390e-173">In **User Attributes** section, click **View and edit all other user attributes** and set hello attributes.</span></span> <span data-ttu-id="2390e-174">Vous devez tooadd une autre revendication nommée **service** et de la valeur de hello doit toobe mappé trop**user.department**.</span><span class="sxs-lookup"><span data-stu-id="2390e-174">You need tooadd another claim named **department** and hello value needs toobe mapped too**user.department**.</span></span>

    | <span data-ttu-id="2390e-175">Nom de l'attribut</span><span class="sxs-lookup"><span data-stu-id="2390e-175">Attribute Name</span></span> | <span data-ttu-id="2390e-176">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="2390e-176">Attribute Value</span></span> |
    | --- | --- |    
    | <span data-ttu-id="2390e-177">department</span><span class="sxs-lookup"><span data-stu-id="2390e-177">department</span></span>| <span data-ttu-id="2390e-178">user.department</span><span class="sxs-lookup"><span data-stu-id="2390e-178">user.department</span></span> |

      ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/userattribute.png)

      <span data-ttu-id="2390e-180">a.</span><span class="sxs-lookup"><span data-stu-id="2390e-180">a.</span></span> <span data-ttu-id="2390e-181">Cliquez sur la page de détails de l’ajouter un attribut tooopen hello attribut ajouter l’attribut hello comme indiqué ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="2390e-181">Click on Add attribute tooopen hello attribute details page add hello department attribute as shown below-</span></span>

      ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/adduserattribute.png)

      <span data-ttu-id="2390e-183">b.</span><span class="sxs-lookup"><span data-stu-id="2390e-183">b.</span></span> <span data-ttu-id="2390e-184">Cliquez sur **Ok** attribut de hello toosave.</span><span class="sxs-lookup"><span data-stu-id="2390e-184">Click on **Ok** toosave hello attribute.</span></span>

      <span data-ttu-id="2390e-185">c.</span><span class="sxs-lookup"><span data-stu-id="2390e-185">c.</span></span> <span data-ttu-id="2390e-186">Modifier le nom d’attribut de hello hello **emailaddress** trop**e-mail**.</span><span class="sxs-lookup"><span data-stu-id="2390e-186">Change hello name of hello attribute **emailaddress** too**email**.</span></span>


10. <span data-ttu-id="2390e-187">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier XML de hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="2390e-187">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello XML file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_certificate.png) 

11. <span data-ttu-id="2390e-189">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="2390e-189">Click **Save**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_400.png)

12. <span data-ttu-id="2390e-191">Accédez trop**paramètres d’administration LinkedIn** section.</span><span class="sxs-lookup"><span data-stu-id="2390e-191">Go too**LinkedIn Admin Settings** section.</span></span> <span data-ttu-id="2390e-192">Télécharger le fichier XML de hello que vous venez de télécharger à partir de hello portail Azure en cliquant sur hello option de fichier XML de télécharger.</span><span class="sxs-lookup"><span data-stu-id="2390e-192">Upload hello XML file you just downloaded from hello Azure portal by clicking on hello Upload XML file option.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_metadata_03.png)

13. <span data-ttu-id="2390e-194">Cliquez sur **sur** tooenable SSO.</span><span class="sxs-lookup"><span data-stu-id="2390e-194">Click **On** tooenable SSO.</span></span> <span data-ttu-id="2390e-195">État de l’authentification unique ne pourra **non connecté** trop**connecté**</span><span class="sxs-lookup"><span data-stu-id="2390e-195">SSO status will change from **Not Connected** too**Connected**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial_linkedin_admin_05.png)

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="2390e-197">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="2390e-197">Creating an Azure AD test user</span></span>
<span data-ttu-id="2390e-198">objectif Hello de cette section est toocreate un utilisateur de test dans le portail de gestion Azure hello appelé Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="2390e-198">hello objective of this section is toocreate a test user in hello Azure Management portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="2390e-200">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2390e-200">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="2390e-201">Bonjour **portail de gestion Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="2390e-201">In hello **Azure Management portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="2390e-203">Accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs** liste de hello toodisplay des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="2390e-203">Go too**Users and groups** and click **All users** toodisplay hello list of users.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="2390e-205">En haut de hello de boîte de dialogue hello, cliquez sur **ajouter** tooopen hello **utilisateur** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="2390e-205">At hello top of hello dialog click **Add** tooopen hello **User** dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="2390e-207">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="2390e-207">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="2390e-209">a.</span><span class="sxs-lookup"><span data-stu-id="2390e-209">a.</span></span> <span data-ttu-id="2390e-210">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="2390e-210">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="2390e-211">b.</span><span class="sxs-lookup"><span data-stu-id="2390e-211">b.</span></span> <span data-ttu-id="2390e-212">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="2390e-212">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="2390e-213">c.</span><span class="sxs-lookup"><span data-stu-id="2390e-213">c.</span></span> <span data-ttu-id="2390e-214">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="2390e-214">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="2390e-215">d.</span><span class="sxs-lookup"><span data-stu-id="2390e-215">d.</span></span> <span data-ttu-id="2390e-216">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="2390e-216">Click **Create**.</span></span> 

### <a name="creating-a-linkedin-elevate-test-user"></a><span data-ttu-id="2390e-217">Création d’un utilisateur test LinkedIn Elevate</span><span class="sxs-lookup"><span data-stu-id="2390e-217">Creating a LinkedIn Elevate test user</span></span>

<span data-ttu-id="2390e-218">Application d’élever lié prend en charge juste configuration en temps utilisateur et une fois que les utilisateurs de l’authentification seront créées automatiquement dans l’application hello.</span><span class="sxs-lookup"><span data-stu-id="2390e-218">Linked Elevate Application supports Just in time user provisioning and after authentication users will be created in hello application automatically.</span></span> <span data-ttu-id="2390e-219">Dans page de paramètres d’administration hello sur le commutateur de portail hello retournement LinkedIn élever hello **automatiquement attribuer des licences** tooactive tooenable juste en temps de préparation et cela affectera également un utilisateur toohello de licence.</span><span class="sxs-lookup"><span data-stu-id="2390e-219">On hello admin settings page on hello LinkedIn Elevate portal flip hello switch **Automatically Assign licenses** tooactive tooenable Just in time provisioning and this will also assign a license toohello user.</span></span>

   ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-linkedinElevate-tutorial/LinkedinUserprovswitch.png)

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="2390e-221">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="2390e-221">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="2390e-222">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant son tooLinkedIn accès élever.</span><span class="sxs-lookup"><span data-stu-id="2390e-222">In this section, you enable Britta Simon toouse Azure single sign-on by granting her access tooLinkedIn Elevate.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="2390e-224">**tooassign Britta Simon tooLinkedIn élever, effectuez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="2390e-224">**tooassign Britta Simon tooLinkedIn Elevate, perform hello following steps:**</span></span>

1. <span data-ttu-id="2390e-225">Dans le portail de gestion Azure hello, ouvrez la vue des applications hello, puis naviguez toohello les vue de répertoire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="2390e-225">In hello Azure Management portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="2390e-227">Dans la liste des applications hello, sélectionnez **LinkedIn élever**.</span><span class="sxs-lookup"><span data-stu-id="2390e-227">In hello applications list, select **LinkedIn Elevate**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-linkedinElevate-tutorial/tutorial-linkedinElevate_0001.png) 

3. <span data-ttu-id="2390e-229">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2390e-229">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="2390e-231">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="2390e-231">Click **Add** button.</span></span> <span data-ttu-id="2390e-232">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2390e-232">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="2390e-234">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="2390e-234">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="2390e-235">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="2390e-235">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="2390e-236">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="2390e-236">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="2390e-237">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="2390e-237">Testing single sign-on</span></span>

<span data-ttu-id="2390e-238">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="2390e-238">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="2390e-239">Lorsque vous cliquez sur hello LinkedIn élever mosaïque hello volet d’accès, vous devez obtenir la page d’authentification Azure hello et sur après authentification réussie, vous devez obtenir dans votre application LinkedIn élever.</span><span class="sxs-lookup"><span data-stu-id="2390e-239">When you click hello LinkedIn Elevate tile in hello Access Panel, you should get hello Azure Sign-on page and on after successful sign-on, you should get into your LinkedIn Elevate application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="2390e-240">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="2390e-240">Additional resources</span></span>

* [<span data-ttu-id="2390e-241">Didacticiel : Configuration de LinkedIn Elevate pour l’approvisionnement automatique d’utilisateurs avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2390e-241">Tutorial: Configuring LinkedIn Elevate for automatic user provisioning with Azure Active Directory</span></span>](active-directory-saas-linkedinelevate-provisioning-tutorial.md)
* [<span data-ttu-id="2390e-242">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="2390e-242">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="2390e-243">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2390e-243">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)


<!--Image references-->

[1]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-linkedinElevate-tutorial/tutorial_general_203.png
