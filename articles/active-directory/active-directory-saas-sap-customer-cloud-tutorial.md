---
title: "Didacticiel : Intégration d’Azure Active Directory à SAP Cloud pour le client | Microsoft Docs"
description: "Découvrez comment tooconfigure l’authentification unique entre Azure Active Directory et de Cloud de SAP pour le client."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 90154dab-eba2-4563-bcf0-f2acc797ea97
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: jeedes
ms.openlocfilehash: 0525ea81122458ab3ac24a5bdb0b5f628405dd05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-azure-active-directory-integration-with-sap-cloud-for-customer"></a><span data-ttu-id="1321d-103">Didacticiel : Intégration d’Azure Active Directory avec SAP Cloud pour le client</span><span class="sxs-lookup"><span data-stu-id="1321d-103">Tutorial: Azure Active Directory integration with SAP Cloud for Customer</span></span>

<span data-ttu-id="1321d-104">Dans ce didacticiel, vous apprendrez comment toointegrate SAP Cloud pour le client avec Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1321d-104">In this tutorial, you learn how toointegrate SAP Cloud for Customer with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="1321d-105">Intégration de Cloud de SAP pour le client auprès d’Azure AD offre hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="1321d-105">Integrating SAP Cloud for Customer with Azure AD provides you with hello following benefits:</span></span>

- <span data-ttu-id="1321d-106">Vous pouvez contrôler dans Azure AD qui a accès tooSAP Cloud pour le client</span><span class="sxs-lookup"><span data-stu-id="1321d-106">You can control in Azure AD who has access tooSAP Cloud for Customer</span></span>
- <span data-ttu-id="1321d-107">Vous pouvez activer vos utilisateurs tooautomatically get connecté tooSAP Cloud pour le client (Single Sign-On) avec leurs comptes Azure AD</span><span class="sxs-lookup"><span data-stu-id="1321d-107">You can enable your users tooautomatically get signed-on tooSAP Cloud for Customer (Single Sign-On) with their Azure AD accounts</span></span>
- <span data-ttu-id="1321d-108">Vous pouvez gérer vos comptes dans un emplacement central : hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="1321d-108">You can manage your accounts in one central location - hello Azure portal</span></span>

<span data-ttu-id="1321d-109">Si vous souhaitez tooknow plus de détails sur l’intégration d’application SaaS à Azure AD, consultez [quel est l’accès à l’application et l’authentification unique avec Azure Active Directory](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="1321d-109">If you want tooknow more details about SaaS app integration with Azure AD, see [what is application access and single sign-on with Azure Active Directory](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1321d-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="1321d-110">Prerequisites</span></span>

<span data-ttu-id="1321d-111">tooconfigure intégration d’Azure AD avec SAP Cloud pour le client, vous devez hello éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="1321d-111">tooconfigure Azure AD integration with SAP Cloud for Customer, you need hello following items:</span></span>

- <span data-ttu-id="1321d-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="1321d-112">An Azure AD subscription</span></span>
- <span data-ttu-id="1321d-113">Un abonnement SAP Cloud for Customer pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="1321d-113">A SAP Cloud for Customer single sign-on enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="1321d-114">tootest hello les étapes de ce didacticiel, nous ne recommandons pas à l’aide d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="1321d-114">tootest hello steps in this tutorial, we do not recommend using a production environment.</span></span>

<span data-ttu-id="1321d-115">tootest hello étapes décrites dans ce didacticiel, vous devez suivre ces recommandations :</span><span class="sxs-lookup"><span data-stu-id="1321d-115">tootest hello steps in this tutorial, you should follow these recommendations:</span></span>

- <span data-ttu-id="1321d-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="1321d-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="1321d-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez obtenir un essai d’un mois ici : [offre d’essai](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1321d-117">If you don't have an Azure AD trial environment, you can get a one-month trial here: [Trial offer](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="1321d-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="1321d-118">Scenario description</span></span>
<span data-ttu-id="1321d-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="1321d-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="1321d-120">scénario Hello décrite dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="1321d-120">hello scenario outlined in this tutorial consists of two main building blocks:</span></span>

1. <span data-ttu-id="1321d-121">Ajout de Cloud de SAP pour le client à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="1321d-121">Adding SAP Cloud for Customer from hello gallery</span></span>
2. <span data-ttu-id="1321d-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1321d-122">Configuring and testing Azure AD single sign-on</span></span>

## <a name="adding-sap-cloud-for-customer-from-hello-gallery"></a><span data-ttu-id="1321d-123">Ajout de Cloud de SAP pour le client à partir de la galerie de hello</span><span class="sxs-lookup"><span data-stu-id="1321d-123">Adding SAP Cloud for Customer from hello gallery</span></span>
<span data-ttu-id="1321d-124">tooconfigure hello intégration de Cloud de SAP pour le client dans Azure AD, vous devez tooadd SAP Cloud pour le client à partir de la liste de tooyour hello Galerie d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="1321d-124">tooconfigure hello integration of SAP Cloud for Customer into Azure AD, you need tooadd SAP Cloud for Customer from hello gallery tooyour list of managed SaaS apps.</span></span>

<span data-ttu-id="1321d-125">**tooadd Cloud SAP pour le client à partir de la galerie hello, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1321d-125">**tooadd SAP Cloud for Customer from hello gallery, perform hello following steps:**</span></span>

1. <span data-ttu-id="1321d-126">Bonjour  **[portail Azure](https://portal.azure.com)**sur hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="1321d-126">In hello **[Azure portal](https://portal.azure.com)**, on hello left navigation panel, click **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="1321d-128">Accédez trop**des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="1321d-128">Navigate too**Enterprise applications**.</span></span> <span data-ttu-id="1321d-129">Passez trop**toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1321d-129">Then go too**All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="1321d-131">tooadd nouvelle application, cliquez sur **nouvelle application** bouton en haut de hello de boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="1321d-131">tooadd new application, click **New application** button on hello top of dialog.</span></span>

    ![Applications][3]

4. <span data-ttu-id="1321d-133">Dans la zone de recherche de hello, tapez **Cloud SAP pour le client**.</span><span class="sxs-lookup"><span data-stu-id="1321d-133">In hello search box, type **SAP Cloud for Customer**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_search.png)

5. <span data-ttu-id="1321d-135">Dans le volet de résultats hello, sélectionnez **Cloud SAP pour le client**, puis cliquez sur **ajouter** bouton application hello de tooadd.</span><span class="sxs-lookup"><span data-stu-id="1321d-135">In hello results panel, select **SAP Cloud for Customer**, and then click **Add** button tooadd hello application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a><span data-ttu-id="1321d-137">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1321d-137">Configuring and testing Azure AD single sign-on</span></span>
<span data-ttu-id="1321d-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec SAP Cloud pour le client, en tirant parti d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="1321d-138">In this section, you configure and test Azure AD single sign-on with SAP Cloud for Customer based on a test user called "Britta Simon".</span></span>

<span data-ttu-id="1321d-139">Pour toowork de l’authentification unique, Azure AD doit tooknow quel utilisateur d’équivalent hello dans le Cloud de SAP pour le client est tooa utilisateur dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1321d-139">For single sign-on toowork, Azure AD needs tooknow what hello counterpart user in SAP Cloud for Customer is tooa user in Azure AD.</span></span> <span data-ttu-id="1321d-140">En d’autres termes, une relation de lien entre un utilisateur Azure AD et un utilisateur hello dans le Cloud de SAP pour le client doit toobe établie.</span><span class="sxs-lookup"><span data-stu-id="1321d-140">In other words, a link relationship between an Azure AD user and hello related user in SAP Cloud for Customer needs toobe established.</span></span>

<span data-ttu-id="1321d-141">Dans le Cloud de SAP pour le client, affecter la valeur hello hello **nom d’utilisateur** dans Azure AD en tant que valeur hello Hello **nom d’utilisateur** relation de lien tooestablish hello.</span><span class="sxs-lookup"><span data-stu-id="1321d-141">In SAP Cloud for Customer, assign hello value of hello **user name** in Azure AD as hello value of hello **Username** tooestablish hello link relationship.</span></span>

<span data-ttu-id="1321d-142">tooconfigure et test Azure AD l’authentification unique avec SAP Cloud pour le client, vous devez hello toocomplete suivant des blocs de construction :</span><span class="sxs-lookup"><span data-stu-id="1321d-142">tooconfigure and test Azure AD single sign-on with SAP Cloud for Customer, you need toocomplete hello following building blocks:</span></span>

1. <span data-ttu-id="1321d-143">**[Configuration d’Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**  -tooenable toouse de vos utilisateurs cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="1321d-143">**[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)** - tooenable your users toouse this feature.</span></span>
2. <span data-ttu-id="1321d-144">**[Création d’un utilisateur de test Azure AD](#creating-an-azure-ad-test-user)**  -tootest Azure AD single sign-on avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="1321d-144">**[Creating an Azure AD test user](#creating-an-azure-ad-test-user)** - tootest Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="1321d-145">**[Création d’un Cloud de SAP pour l’utilisateur de test client](#creating-a-sap-cloud-for-customer-test-user)**  -toohave un équivalent de Britta Simon dans le Cloud de SAP pour le client qui est la représentation sous forme de toohello lié Azure AD de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="1321d-145">**[Creating a SAP Cloud for Customer test user](#creating-a-sap-cloud-for-customer-test-user)** - toohave a counterpart of Britta Simon in SAP Cloud for Customer that is linked toohello Azure AD representation of user.</span></span>
4. <span data-ttu-id="1321d-146">**[Utilisateur de test affectation hello Azure AD](#assigning-the-azure-ad-test-user)**  -tooenable Britta Simon toouse Azure AD de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1321d-146">**[Assigning hello Azure AD test user](#assigning-the-azure-ad-test-user)** - tooenable Britta Simon toouse Azure AD single sign-on.</span></span>
5. <span data-ttu-id="1321d-147">**[Test de l’authentification unique sur](#testing-single-sign-on)**  -tooverify hello indique si les tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="1321d-147">**[Testing Single Sign-On](#testing-single-sign-on)** - tooverify whether hello configuration works.</span></span>

### <a name="configuring-azure-ad-single-sign-on"></a><span data-ttu-id="1321d-148">Configuration de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="1321d-148">Configuring Azure AD single sign-on</span></span>

<span data-ttu-id="1321d-149">Dans cette section, vous activez Azure AD l’authentification unique sur Bonjour portail Azure et configurez l’authentification unique dans votre Cloud de SAP pour l’application du client.</span><span class="sxs-lookup"><span data-stu-id="1321d-149">In this section, you enable Azure AD single sign-on in hello Azure portal and configure single sign-on in your SAP Cloud for Customer application.</span></span>

<span data-ttu-id="1321d-150">**tooconfigure Azure AD l’authentification unique avec le Cloud de SAP pour le client, exécutez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1321d-150">**tooconfigure Azure AD single sign-on with SAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="1321d-151">Bonjour portail Azure, sur hello **Cloud SAP pour le client** page d’intégration d’application, cliquez sur **l’authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="1321d-151">In hello Azure portal, on hello **SAP Cloud for Customer** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="1321d-153">Sur hello **l’authentification unique** boîte de dialogue, sélectionnez **Mode** en tant que **SAML-authentification** tooenable l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1321d-153">On hello **Single sign-on** dialog, select **Mode** as   **SAML-based Sign-on** tooenable single sign-on.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_samlbase.png)

3. <span data-ttu-id="1321d-155">Sur hello **Cloud SAP pour le domaine du client et les URL** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1321d-155">On hello **SAP Cloud for Customer Domain and URLs** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_url.png)

    <span data-ttu-id="1321d-157">a.</span><span class="sxs-lookup"><span data-stu-id="1321d-157">a.</span></span> <span data-ttu-id="1321d-158">Bonjour **URL de connexion** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="1321d-158">In hello **Sign-on URL** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    <span data-ttu-id="1321d-159">b.</span><span class="sxs-lookup"><span data-stu-id="1321d-159">b.</span></span> <span data-ttu-id="1321d-160">Bonjour **identificateur** zone de texte, tapez une URL à l’aide de hello modèle :`https://<server name>.crm.ondemand.com`</span><span class="sxs-lookup"><span data-stu-id="1321d-160">In hello **Identifier** textbox, type a URL using hello following pattern: `https://<server name>.crm.ondemand.com`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="1321d-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="1321d-161">These values are not real.</span></span> <span data-ttu-id="1321d-162">Mettre à jour les valeurs de hello réel Sign-On URL et l’identificateur.</span><span class="sxs-lookup"><span data-stu-id="1321d-162">Update these values with hello actual Sign-On URL and Identifier.</span></span> <span data-ttu-id="1321d-163">Contact [Cloud SAP pour l’équipe de support technique Client](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="1321d-163">Contact [SAP Cloud for Customer Client support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooget these values.</span></span> 

4. <span data-ttu-id="1321d-164">Sur hello **attributs utilisateur** section, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1321d-164">On hello **User Attributes** section, perform hello following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_attribute.png)

    <span data-ttu-id="1321d-166">a.</span><span class="sxs-lookup"><span data-stu-id="1321d-166">a.</span></span> <span data-ttu-id="1321d-167">Dans **identificateur de l’utilisateur** liste, sélectionnez hello **ExtractMailPrefix()** (fonction).</span><span class="sxs-lookup"><span data-stu-id="1321d-167">In **User Identifier** list, select hello **ExtractMailPrefix()** function.</span></span>

    <span data-ttu-id="1321d-168">b.</span><span class="sxs-lookup"><span data-stu-id="1321d-168">b.</span></span> <span data-ttu-id="1321d-169">À partir de hello **Mail** liste, sélectionnez hello utilisateur attribut toouse pour votre implémentation.</span><span class="sxs-lookup"><span data-stu-id="1321d-169">From hello **Mail** list, select hello user attribute you want toouse for your implementation.</span></span>
    <span data-ttu-id="1321d-170">Par exemple, si vous voulez toouse hello EmployeeID comme identificateur d’utilisateur unique et si vous avez stocké la valeur de l’attribut hello Bonjour ExtensionAttribute2, puis sélectionnez user.extensionattribute2.</span><span class="sxs-lookup"><span data-stu-id="1321d-170">For example, if you want toouse hello EmployeeID as unique user identifier and you have stored hello attribute value in hello ExtensionAttribute2, then select user.extensionattribute2.</span></span>  

5. <span data-ttu-id="1321d-171">Sur hello **le certificat de signature SAML** , cliquez sur **Metadata XML** , puis enregistrez le fichier de métadonnées hello sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="1321d-171">On hello **SAML Signing Certificate** section, click **Metadata XML** and then save hello metadata file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_certificate.png) 

6. <span data-ttu-id="1321d-173">Cliquez sur le bouton **Enregistrer** .</span><span class="sxs-lookup"><span data-stu-id="1321d-173">Click **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_400.png)

7. <span data-ttu-id="1321d-175">Sur hello **Cloud SAP pour la Configuration de client** , cliquez sur **configurer le Cloud SAP pour le client** tooopen **configurer l’authentification** fenêtre.</span><span class="sxs-lookup"><span data-stu-id="1321d-175">On hello **SAP Cloud for Customer Configuration** section, click **Configure SAP Cloud for Customer** tooopen **Configure sign-on** window.</span></span> <span data-ttu-id="1321d-176">Hello de copie **SAML Sign-On URL du Service unique** de hello **section de référence rapide.**</span><span class="sxs-lookup"><span data-stu-id="1321d-176">Copy hello **SAML Single Sign-On Service URL** from hello **Quick Reference section.**</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_configure.png) 

8. <span data-ttu-id="1321d-178">tooget l’authentification unique configurée, procédez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1321d-178">tooget SSO configured, perform hello following steps:</span></span>
   
    <span data-ttu-id="1321d-179">a.</span><span class="sxs-lookup"><span data-stu-id="1321d-179">a.</span></span> <span data-ttu-id="1321d-180">Connectez-vous au portail SAP Cloud pour le client avec des droits d’administrateur.</span><span class="sxs-lookup"><span data-stu-id="1321d-180">Login into SAP Cloud for Customer portal with administrator rights.</span></span>
   
    <span data-ttu-id="1321d-181">b.</span><span class="sxs-lookup"><span data-stu-id="1321d-181">b.</span></span> <span data-ttu-id="1321d-182">Accédez toohello **Application et la tâche courante de gestion utilisateur** et cliquez sur hello **fournisseur d’identité** onglet.</span><span class="sxs-lookup"><span data-stu-id="1321d-182">Navigate toohello **Application and User Management Common Task** and click hello **Identity Provider** tab.</span></span>
   
    <span data-ttu-id="1321d-183">c.</span><span class="sxs-lookup"><span data-stu-id="1321d-183">c.</span></span> <span data-ttu-id="1321d-184">Cliquez sur **nouveau fournisseur d’identité** et le fichier XML des métadonnées hello select que vous avez téléchargé à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1321d-184">Click **New Identity Provider** and select hello metadata XML file you have downloaded from hello Azure portal.</span></span> <span data-ttu-id="1321d-185">En important des métadonnées de hello, système de hello télécharge automatiquement le certificat de signature requis hello et certificat de chiffrement.</span><span class="sxs-lookup"><span data-stu-id="1321d-185">By importing hello metadata, hello system automatically uploads hello required signature certificate and encryption certificate.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_54.png)
   
    <span data-ttu-id="1321d-187">d.</span><span class="sxs-lookup"><span data-stu-id="1321d-187">d.</span></span> <span data-ttu-id="1321d-188">Azure Active Directory requiert élément hello Assertion Consumer Service URL dans la demande SAML hello, afin de le sélectionner hello **inclure l’URL Assertion Consumer Service** case à cocher.</span><span class="sxs-lookup"><span data-stu-id="1321d-188">Azure Active Directory requires hello element Assertion Consumer Service URL in hello SAML request, so select hello **Include Assertion Consumer Service URL** checkbox.</span></span>
   
    <span data-ttu-id="1321d-189">e.</span><span class="sxs-lookup"><span data-stu-id="1321d-189">e.</span></span> <span data-ttu-id="1321d-190">Cliquez sur **Activate Single Sign-On**(Activer l’authentification unique).</span><span class="sxs-lookup"><span data-stu-id="1321d-190">Click **Activate Single Sign-On**.</span></span>
   
    <span data-ttu-id="1321d-191">f.</span><span class="sxs-lookup"><span data-stu-id="1321d-191">f.</span></span> <span data-ttu-id="1321d-192">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="1321d-192">Save your changes.</span></span>
   
    <span data-ttu-id="1321d-193">g.</span><span class="sxs-lookup"><span data-stu-id="1321d-193">g.</span></span> <span data-ttu-id="1321d-194">Cliquez sur hello **mon système** onglet.</span><span class="sxs-lookup"><span data-stu-id="1321d-194">Click hello **My System** tab.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_52.png)
   
    <span data-ttu-id="1321d-196">h.</span><span class="sxs-lookup"><span data-stu-id="1321d-196">h.</span></span> <span data-ttu-id="1321d-197">Dans la zone de texte **Azure AD Sign On URL** (URL de connexion Azure AD), collez l’**URL du service d’authentification unique SAML** que vous avez copiée à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="1321d-197">In **Azure AD Sign On URL** textbox, paste **SAML Single Sign-On Service URL** which you have copied from Azure portal.</span></span>
   
    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_53.png)
   
    <span data-ttu-id="1321d-199">i.</span><span class="sxs-lookup"><span data-stu-id="1321d-199">i.</span></span> <span data-ttu-id="1321d-200">Spécifier si les employés hello peuvent manuellement choisir entre l’ouverture de session avec l’ID d’utilisateur et mot de passe ou l’authentification unique en sélectionnant hello **sélection de fournisseur d’identité manuelle**.</span><span class="sxs-lookup"><span data-stu-id="1321d-200">Specify whether hello employee can manually choose between logging on with user ID and password or SSO by selecting hello **Manual Identity Provider Selection**.</span></span>
   
    <span data-ttu-id="1321d-201">j.</span><span class="sxs-lookup"><span data-stu-id="1321d-201">j.</span></span> <span data-ttu-id="1321d-202">Bonjour **URL SSO** section, spécifiez les URL hello qui doit être utilisé par votre toosign employés sur toohello système.</span><span class="sxs-lookup"><span data-stu-id="1321d-202">In hello **SSO URL** section, specify hello URL that should be used by your employees toosign on toohello system.</span></span> 
    <span data-ttu-id="1321d-203">Bonjour **tooEmployee d’URL envoyée** la liste, vous pouvez choisir entre hello options suivantes :</span><span class="sxs-lookup"><span data-stu-id="1321d-203">In hello **URL Sent tooEmployee** list, you can choose between hello following options:</span></span>
   
    <span data-ttu-id="1321d-204">**Non-SSO URL**</span><span class="sxs-lookup"><span data-stu-id="1321d-204">**Non-SSO URL**</span></span>
   
    <span data-ttu-id="1321d-205">système de Hello envoie employé toohello hello uniquement des URL de normal du système.</span><span class="sxs-lookup"><span data-stu-id="1321d-205">hello system sends only hello normal system URL toohello employee.</span></span> <span data-ttu-id="1321d-206">employé de Hello ne peut pas se connecter à l’aide de l’authentification unique et doit utiliser le mot de passe ou de certificats à la place.</span><span class="sxs-lookup"><span data-stu-id="1321d-206">hello employee cannot log on using SSO, and must use password or certificate instead.</span></span>
   
    <span data-ttu-id="1321d-207">**URL SSO**</span><span class="sxs-lookup"><span data-stu-id="1321d-207">**SSO URL**</span></span> 
   
    <span data-ttu-id="1321d-208">système de Hello envoie uniquement les employés de toohello URL SSO hello.</span><span class="sxs-lookup"><span data-stu-id="1321d-208">hello system sends only hello SSO URL toohello employee.</span></span> <span data-ttu-id="1321d-209">les employés Hello peuvent se connecter à l’aide de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="1321d-209">hello employee can log on using SSO.</span></span> <span data-ttu-id="1321d-210">Demande d’authentification est redirigée via hello IdP.</span><span class="sxs-lookup"><span data-stu-id="1321d-210">Authentication request is redirected through hello IdP.</span></span>
   
    <span data-ttu-id="1321d-211">**Sélection automatique**</span><span class="sxs-lookup"><span data-stu-id="1321d-211">**Automatic Selection**</span></span>
   
    <span data-ttu-id="1321d-212">Si l’authentification unique n’est pas actif, système de hello envoie employé de toohello URL hello normal du système.</span><span class="sxs-lookup"><span data-stu-id="1321d-212">If SSO is not active, hello system sends hello normal system URL toohello employee.</span></span> <span data-ttu-id="1321d-213">Si l’authentification unique est actif, système de hello vérifie si les employés hello a un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="1321d-213">If SSO is active, hello system checks whether hello employee has a password.</span></span> <span data-ttu-id="1321d-214">Si un mot de passe est disponible, les URL d’authentification unique et Non-SSO URL sont envoyées toohello employé.</span><span class="sxs-lookup"><span data-stu-id="1321d-214">If a password is available, both SSO URL and Non-SSO URL are sent toohello employee.</span></span> <span data-ttu-id="1321d-215">Toutefois, si l’employé de hello n’a aucun mot de passe, uniquement hello URL d’authentification unique est envoyé toohello employé.</span><span class="sxs-lookup"><span data-stu-id="1321d-215">However, if hello employee has no password, only hello SSO URL is sent toohello employee.</span></span>
   
    <span data-ttu-id="1321d-216">k.</span><span class="sxs-lookup"><span data-stu-id="1321d-216">k.</span></span> <span data-ttu-id="1321d-217">Enregistrez vos modifications.</span><span class="sxs-lookup"><span data-stu-id="1321d-217">Save your changes.</span></span>

> [!TIP]
> <span data-ttu-id="1321d-218">Vous pouvez maintenant lire une version concise de ces instructions à l’intérieur de hello [portail Azure](https://portal.azure.com), lors de la configuration de l’application hello !</span><span class="sxs-lookup"><span data-stu-id="1321d-218">You can now read a concise version of these instructions inside hello [Azure portal](https://portal.azure.com), while you are setting up hello app!</span></span>  <span data-ttu-id="1321d-219">Après l’ajout de cette application à partir de hello **Active Directory > Applications d’entreprise** , cliquez simplement sur hello **Single Sign-On** hello onglet et accès incorporé documentation via hello  **Configuration** section bas hello.</span><span class="sxs-lookup"><span data-stu-id="1321d-219">After adding this app from hello **Active Directory > Enterprise Applications** section, simply click hello **Single Sign-On** tab and access hello embedded documentation through hello **Configuration** section at hello bottom.</span></span> <span data-ttu-id="1321d-220">Vous pouvez en savoir plus sur la fonctionnalité de documentation embedded hello ici : [Azure AD incorporé documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span><span class="sxs-lookup"><span data-stu-id="1321d-220">You can read more about hello embedded documentation feature here: [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985)</span></span>
> 

### <a name="creating-an-azure-ad-test-user"></a><span data-ttu-id="1321d-221">Création d’un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="1321d-221">Creating an Azure AD test user</span></span>
<span data-ttu-id="1321d-222">objectif Hello de cette section est toocreate Bonjour Azure portal appelé Britta Simon, un utilisateur de test.</span><span class="sxs-lookup"><span data-stu-id="1321d-222">hello objective of this section is toocreate a test user in hello Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="1321d-224">**toocreate un utilisateur test dans Azure AD, procédez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1321d-224">**toocreate a test user in Azure AD, perform hello following steps:**</span></span>

1. <span data-ttu-id="1321d-225">Bonjour **portail Azure**, on hello du volet de navigation gauche, cliquez sur **Azure Active Directory** icône.</span><span class="sxs-lookup"><span data-stu-id="1321d-225">In hello **Azure portal**, on hello left navigation pane, click **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="1321d-227">liste de hello toodisplay des utilisateurs, accédez trop**utilisateurs et groupes** et cliquez sur **tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="1321d-227">toodisplay hello list of users, go too**Users and groups** and click **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="1321d-229">tooopen hello **utilisateur** boîte de dialogue, cliquez sur **ajouter** haut hello de boîte de dialogue hello.</span><span class="sxs-lookup"><span data-stu-id="1321d-229">tooopen hello **User** dialog, click **Add** on hello top of hello dialog.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="1321d-231">Sur hello **utilisateur** boîte de dialogue de page, effectuer hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="1321d-231">On hello **User** dialog page, perform hello following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-sap-customer-cloud-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="1321d-233">a.</span><span class="sxs-lookup"><span data-stu-id="1321d-233">a.</span></span> <span data-ttu-id="1321d-234">Bonjour **nom** zone de texte, type **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="1321d-234">In hello **Name** textbox, type **BrittaSimon**.</span></span>

    <span data-ttu-id="1321d-235">b.</span><span class="sxs-lookup"><span data-stu-id="1321d-235">b.</span></span> <span data-ttu-id="1321d-236">Bonjour **nom d’utilisateur** hello de type zone de texte **adresse de messagerie** de BrittaSimon.</span><span class="sxs-lookup"><span data-stu-id="1321d-236">In hello **User name** textbox, type hello **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="1321d-237">c.</span><span class="sxs-lookup"><span data-stu-id="1321d-237">c.</span></span> <span data-ttu-id="1321d-238">Sélectionnez **afficher le mot de passe** et notez la valeur hello hello **mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="1321d-238">Select **Show Password** and write down hello value of hello **Password**.</span></span>

    <span data-ttu-id="1321d-239">d.</span><span class="sxs-lookup"><span data-stu-id="1321d-239">d.</span></span> <span data-ttu-id="1321d-240">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="1321d-240">Click **Create**.</span></span>
 
### <a name="creating-a-sap-cloud-for-customer-test-user"></a><span data-ttu-id="1321d-241">Création d’un utilisateur de test SAP Cloud for Customer</span><span class="sxs-lookup"><span data-stu-id="1321d-241">Creating a SAP Cloud for Customer test user</span></span>

<span data-ttu-id="1321d-242">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans SAP Cloud pour le client.</span><span class="sxs-lookup"><span data-stu-id="1321d-242">In this section, you create a user called Britta Simon in SAP Cloud for Customer.</span></span> <span data-ttu-id="1321d-243">Collaborez avec [Cloud SAP pour l’équipe du support technique](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) utilisateurs hello tooadd hello SAP Cloud pour la plateforme du client.</span><span class="sxs-lookup"><span data-stu-id="1321d-243">Please work with [SAP Cloud for Customer support team](https://www.sap.com/about/agreements.sap-cloud-services-customers.html) tooadd hello users in hello SAP Cloud for Customer platform.</span></span> 

> [!NOTE]
> <span data-ttu-id="1321d-244">Assurez-vous que NameID valeur doit correspondre au champ de nom d’utilisateur hello Bonjour SAP Cloud pour la plateforme du client.</span><span class="sxs-lookup"><span data-stu-id="1321d-244">Please make sure that NameID value should match with hello username field in hello SAP Cloud for Customer platform.</span></span>

### <a name="assigning-hello-azure-ad-test-user"></a><span data-ttu-id="1321d-245">Affectation d’utilisateur de test hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="1321d-245">Assigning hello Azure AD test user</span></span>

<span data-ttu-id="1321d-246">Dans cette section, vous activez toouse Britta Simon Azure l’authentification unique en accordant l’accès tooSAP Cloud pour le client.</span><span class="sxs-lookup"><span data-stu-id="1321d-246">In this section, you enable Britta Simon toouse Azure single sign-on by granting access tooSAP Cloud for Customer.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="1321d-248">**tooassign Britta Simon tooSAP Cloud pour le client, exécutez hello comme suit :**</span><span class="sxs-lookup"><span data-stu-id="1321d-248">**tooassign Britta Simon tooSAP Cloud for Customer, perform hello following steps:**</span></span>

1. <span data-ttu-id="1321d-249">Bonjour portail Azure, ouvrez la vue des applications hello, puis naviguez toohello vue d’annuaire et accédez trop**des applications d’entreprise** puis cliquez sur **toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="1321d-249">In hello Azure portal, open hello applications view, and then navigate toohello directory view and go too**Enterprise applications** then click **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="1321d-251">Dans la liste des applications hello, sélectionnez **Cloud SAP pour le client**.</span><span class="sxs-lookup"><span data-stu-id="1321d-251">In hello applications list, select **SAP Cloud for Customer**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_sapcloudforcustomer_app.png) 

3. <span data-ttu-id="1321d-253">Dans le menu hello hello gauche, cliquez sur **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1321d-253">In hello menu on hello left, click **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="1321d-255">Cliquez sur le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="1321d-255">Click **Add** button.</span></span> <span data-ttu-id="1321d-256">Ensuite, sélectionnez **Utilisateurs et groupes** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1321d-256">Then select **Users and groups** on **Add Assignment** dialog.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="1321d-258">Sur **utilisateurs et groupes** boîte de dialogue, sélectionnez **Britta Simon** dans la liste des utilisateurs hello.</span><span class="sxs-lookup"><span data-stu-id="1321d-258">On **Users and groups** dialog, select **Britta Simon** in hello Users list.</span></span>

6. <span data-ttu-id="1321d-259">Cliquez sur le bouton **Sélectionner** dans la boîte de dialogue **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="1321d-259">Click **Select** button on **Users and groups** dialog.</span></span>

7. <span data-ttu-id="1321d-260">Cliquez sur le bouton **Affecter** dans la boîte de dialogue **Ajouter une affectation**.</span><span class="sxs-lookup"><span data-stu-id="1321d-260">Click **Assign** button on **Add Assignment** dialog.</span></span>
    
### <a name="testing-single-sign-on"></a><span data-ttu-id="1321d-261">Test de l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="1321d-261">Testing single sign-on</span></span>

<span data-ttu-id="1321d-262">Dans cette section, vous tester votre configuration Azure AD unique de session à l’aide de hello panneau d’accès.</span><span class="sxs-lookup"><span data-stu-id="1321d-262">In this section, you test your Azure AD single sign-on configuration using hello Access Panel.</span></span>

<span data-ttu-id="1321d-263">Lorsque vous cliquez sur hello SAP Cloud pour mosaïque hello volet d’accès client, vous devez obtenir automatiquement signé sur tooyour SAP Cloud pour l’application du client.</span><span class="sxs-lookup"><span data-stu-id="1321d-263">When you click hello SAP Cloud for Customer tile in hello Access Panel, you should get automatically signed-on tooyour SAP Cloud for Customer application.</span></span>
<span data-ttu-id="1321d-264">Pour plus d’informations sur hello volet d’accès, consultez [Introduction toohello volet d’accès](active-directory-saas-access-panel-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="1321d-264">For more information about hello Access Panel, see [Introduction toohello Access Panel](active-directory-saas-access-panel-introduction.md).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="1321d-265">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="1321d-265">Additional resources</span></span>

* [<span data-ttu-id="1321d-266">Liste des didacticiels sur la façon de tooIntegrate les applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1321d-266">List of Tutorials on How tooIntegrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="1321d-267">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="1321d-267">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-sap-customer-cloud-tutorial/tutorial_general_203.png

