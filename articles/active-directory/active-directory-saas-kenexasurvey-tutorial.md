---
title: "Didacticiel : intégration d’Azure Active Directory à IBM Kenexa Survey Enterprise | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et IBM Kenexa Survey Enterprise."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: c7aac6da-f4bf-419e-9e1a-16b460641a52
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2017
ms.author: jeedes
ms.openlocfilehash: 5c276c23288292a1c54dd9d57177d5072b90c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-ibm-kenexa-survey-enterprise"></a><span data-ttu-id="53cbb-103">Didacticiel : intégration d’Azure Active Directory à IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="53cbb-103">Tutorial: Azure Active Directory integration with IBM Kenexa Survey Enterprise</span></span>

<span data-ttu-id="53cbb-104">Dans ce didacticiel, vous allez apprendre à intégrer IBM Kenexa Survey Enterprise à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="53cbb-104">In this tutorial, you learn how to integrate IBM Kenexa Survey Enterprise with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="53cbb-105">L’intégration du logiciel IBM Kenexa Survey Enterprise à Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="53cbb-105">Integrating IBM Kenexa Survey Enterprise with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="53cbb-106">Dans Azure AD, vous pouvez contrôler qui a accès à IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="53cbb-106">You can control in Azure AD who has access to IBM Kenexa Survey Enterprise.</span></span>
- <span data-ttu-id="53cbb-107">Vous pouvez autoriser vos utilisateurs à se connecter automatiquement à IBM Kenexa Survey Enterprise en utilisant une authentification unique (SSO) avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53cbb-107">You can enable your users to automatically sign in to IBM Kenexa Survey Enterprise by using single sign-on (SSO) with their Azure AD accounts.</span></span>
- <span data-ttu-id="53cbb-108">Vous pouvez gérer vos comptes dans un emplacement central : le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="53cbb-108">You can manage your accounts in one central location: the Azure portal.</span></span>

<span data-ttu-id="53cbb-109">Pour plus d’informations sur l’intégration d’applications SaaS (software as a service) à Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="53cbb-109">If you want to know more about software as a service (SaaS) app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53cbb-110">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="53cbb-110">Prerequisites</span></span>

<span data-ttu-id="53cbb-111">Pour configurer l’intégration d’Azure AD à IBM Kenexa Survey Enterprise, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="53cbb-111">To configure Azure AD integration with IBM Kenexa Survey Enterprise, you need the following items:</span></span>

- <span data-ttu-id="53cbb-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="53cbb-112">An Azure AD subscription</span></span>
- <span data-ttu-id="53cbb-113">Un abonnement IBM Kenexa Survey Enterprise pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="53cbb-113">An IBM Kenexa Survey Enterprise SSO-enabled subscription</span></span>

> [!NOTE]
> <span data-ttu-id="53cbb-114">Lorsque vous testez les étapes de ce didacticiel, nous déconseillons l’utilisation d’un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="53cbb-114">When you test the steps in this tutorial, we recommend that you do not use a production environment.</span></span>

<span data-ttu-id="53cbb-115">Pour tester la procédure de ce didacticiel, suivez les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="53cbb-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="53cbb-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="53cbb-116">Do not use your production environment, unless it is necessary.</span></span>
- <span data-ttu-id="53cbb-117">Si vous n’avez pas d’environnement d’essai Azure AD, vous pouvez [obtenir un essai d’un mois](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="53cbb-117">If you don't have an Azure AD trial environment, you can [get a one-month trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="scenario-description"></a><span data-ttu-id="53cbb-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="53cbb-118">Scenario description</span></span>
<span data-ttu-id="53cbb-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="53cbb-119">In this tutorial, you test Azure AD SSO in a test environment.</span></span> <span data-ttu-id="53cbb-120">Le scénario décrit dans ce didacticiel se compose de deux blocs de construction principaux :</span><span class="sxs-lookup"><span data-stu-id="53cbb-120">The scenario outlined in the tutorial consists of two main building blocks:</span></span>

* <span data-ttu-id="53cbb-121">Ajout de l’application IBM Kenexa Survey Enterprise à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="53cbb-121">Adding IBM Kenexa Survey Enterprise from the gallery</span></span>
* <span data-ttu-id="53cbb-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="53cbb-122">Configuring and testing Azure AD SSO</span></span>

## <a name="add-ibm-kenexa-survey-enterprise-from-the-gallery"></a><span data-ttu-id="53cbb-123">Ajouter l’application IBM Kenexa Survey Enterprise à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="53cbb-123">Add IBM Kenexa Survey Enterprise from the gallery</span></span>
<span data-ttu-id="53cbb-124">Pour configurer l’intégration d’IBM Kenexa Survey Enterprise à Azure AD, vous devez l’ajouter à votre liste d’applications SaaS managées à partir de la galerie.</span><span class="sxs-lookup"><span data-stu-id="53cbb-124">To configure the integration of IBM Kenexa Survey Enterprise into Azure AD, add IBM Kenexa Survey Enterprise from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="53cbb-125">Pour ajouter IBM Kenexa Survey Enterprise à partir de la galerie, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="53cbb-125">To add IBM Kenexa Survey Enterprise from the gallery, do the following:</span></span>

1. <span data-ttu-id="53cbb-126">Dans le volet gauche du [portail Azure](https://portal.azure.com), cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-126">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Active Directory** button.</span></span> 

    ![Bouton Azure Active Directory][1]

2. <span data-ttu-id="53cbb-128">Sélectionnez **Applications d’entreprise**, puis **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-128">Select **Enterprise applications**, and then select **All applications**.</span></span>

    ![Panneau Applications d’entreprise][2]
    
3. <span data-ttu-id="53cbb-130">Pour ajouter une application, cliquez sur le bouton **Nouvelle application**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-130">To add an application, click the **New application** button.</span></span>

    ![Bouton Nouvelle application][3]

4. <span data-ttu-id="53cbb-132">Dans la zone de recherche, tapez **IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-132">In the search box, type **IBM Kenexa Survey Enterprise**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_search.png)

5. <span data-ttu-id="53cbb-134">Dans la liste des résultats, sélectionnez **IBM Kenexa Survey Enterprise**, puis cliquez sur le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="53cbb-134">In the results list, select **IBM Kenexa Survey Enterprise**, and then click the **Add** button to add the application.</span></span>

    ![IBM Kenexa Survey Enterprise dans la liste des résultats](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="53cbb-136">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="53cbb-136">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="53cbb-137">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec IBM Kenexa Survey Enterprise au moyen d’un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="53cbb-137">In this section, you configure and test Azure AD SSO with IBM Kenexa Survey Enterprise based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="53cbb-138">Pour que l’authentification unique fonctionne, Azure AD doit identifier l’utilisateur équivalent à l’utilisateur Azure AD dans IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="53cbb-138">For SSO to work, Azure AD needs to identify the IBM Kenexa Survey Enterprise user counterpart in Azure AD.</span></span> <span data-ttu-id="53cbb-139">En d’autres termes, Azure AD doit établir un lien entre un utilisateur Azure AD et un utilisateur associé dans IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="53cbb-139">In other words, Azure AD must establish a link relationship between an Azure AD user and a related user in IBM Kenexa Survey Enterprise.</span></span>

<span data-ttu-id="53cbb-140">Pour établir la relation de lien, assignez la valeur du **nom d’utilisateur** dans IBM Kenexa Survey Enterprise en tant que de **nom d’utilisateur** dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53cbb-140">To establish the link relationship, assign the value of the **user name** in IBM Kenexa Survey Enterprise as the value of the **Username** in Azure AD.</span></span>

<span data-ttu-id="53cbb-141">Pour configurer et tester l’authentification unique Azure AD auprès d’IBM Kenexa Survey Enterprise, reportez-vous aux blocs de construction des deux sections suivantes.</span><span class="sxs-lookup"><span data-stu-id="53cbb-141">To configure and test Azure AD SSO with IBM Kenexa Survey Enterprise, complete the building blocks in the next two sections.</span></span>

### <a name="configure-azure-ad-sso"></a><span data-ttu-id="53cbb-142">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="53cbb-142">Configure Azure AD SSO</span></span>

<span data-ttu-id="53cbb-143">Dans cette section, vous allez activer l’authentification unique (SSO) Azure AD dans le portail Azure et la configurer dans votre application IBM Kenexa Survey Enterprise en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="53cbb-143">In this section, you enable Azure AD SSO in the Azure portal and configure SSO in your IBM Kenexa Survey Enterprise application by doing the following:</span></span>

1. <span data-ttu-id="53cbb-144">Dans le portail Azure, sur la page d’intégration de l’application **IBM Kenexa Survey Enterprise**, cliquez sur **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-144">In the Azure portal, on the **IBM Kenexa Survey Enterprise** application integration page, click **Single sign-on**.</span></span>

    ![Configurer l’authentification unique dans IBM Kenexa Survey Enterprise][4]

2. <span data-ttu-id="53cbb-146">Dans la boîte de dialogue **Authentification unique**, dans la zone **Mode**, sélectionnez **Authentification basée sur SAML** pour activer l’authentification unique (SSO).</span><span class="sxs-lookup"><span data-stu-id="53cbb-146">In the **Single sign-on** dialog box, in the **Mode** box, select **SAML-based Sign-on** to enable SSO.</span></span>
 
    ![Boîte de dialogue Authentification unique](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_samlbase.png)

3. <span data-ttu-id="53cbb-148">Dans la section **Domaine et URL IBM Kenexa Survey Enterprise**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="53cbb-148">In the **IBM Kenexa Survey Enterprise Domain and URLs** section, perform the following steps:</span></span>

    ![Informations d’authentification unique de domaine et d’URL d’IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_url.png)

    <span data-ttu-id="53cbb-150">a.</span><span class="sxs-lookup"><span data-stu-id="53cbb-150">a.</span></span> <span data-ttu-id="53cbb-151">Dans la zone de texte **Identificateur**, entrez un URL au format suivant : `https://surveys.kenexa.com/<companycode>`</span><span class="sxs-lookup"><span data-stu-id="53cbb-151">In the **Identifier** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>`</span></span>

    <span data-ttu-id="53cbb-152">b.</span><span class="sxs-lookup"><span data-stu-id="53cbb-152">b.</span></span> <span data-ttu-id="53cbb-153">Dans la zone de texte **URL de réponse**, tapez une URL au format suivant : `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span><span class="sxs-lookup"><span data-stu-id="53cbb-153">In the **Reply URL** textbox, type a URL with the following pattern: `https://surveys.kenexa.com/<companycode>/tools/sso.asp`</span></span>

    > [!NOTE] 
    > <span data-ttu-id="53cbb-154">Les valeurs ci-dessus ne sont pas réelles.</span><span class="sxs-lookup"><span data-stu-id="53cbb-154">The preceding values are not real.</span></span> <span data-ttu-id="53cbb-155">Mettez-les à jour avec l’identificateur et l’URL de réponse réels.</span><span class="sxs-lookup"><span data-stu-id="53cbb-155">Update them with the actual identifier and reply URL.</span></span> <span data-ttu-id="53cbb-156">Pour obtenir les valeurs réelles, contactez l’[équipe de support technique d’IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="53cbb-156">To obtain the actual values, contact the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

4. <span data-ttu-id="53cbb-157">Sous **Certificat de signature SAML**, cliquez sur **Certificat (en base64)**, puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="53cbb-157">Under **SAML Signing Certificate**, click **Certificate (Base64)**, and then save the certificate file to your computer.</span></span>

    ![Lien de téléchargement du certificat (en base64)](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_certificate.png) 

    <span data-ttu-id="53cbb-159">L’application IBM Kenexa Survey Enterprise s’attend à recevoir les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à la configuration des attributs de votre jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="53cbb-159">The IBM Kenexa Survey Enterprise application expects to receive the Security Assertions Markup Language (SAML) assertions in a specific format, which requires you to add custom attribute mappings to the configuration of your SAML token attributes.</span></span> <span data-ttu-id="53cbb-160">La valeur de la revendication d’identificateur d’utilisateur dans la réponse doit correspondre à l’ID SSO configuré dans le système Kenexa.</span><span class="sxs-lookup"><span data-stu-id="53cbb-160">The value of the user-identifier claim in the response must match the SSO ID that's configured in the Kenexa system.</span></span> <span data-ttu-id="53cbb-161">Pour mapper l’identificateur d’utilisateur approprié dans votre organisation en tant que protocole IDP (Internet Datagram Protocol) d’authentification unique, collaborez avec l’[équipe de support technique IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="53cbb-161">To map the appropriate user identifier in your organization as SSO Internet Datagram Protocol (IDP), work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> 

    <span data-ttu-id="53cbb-162">Par défaut, AD Azure définit l’identificateur d’utilisateur en tant que valeur de nom d’utilisateur principal (UPN).</span><span class="sxs-lookup"><span data-stu-id="53cbb-162">By default, Azure AD sets the user identifier as the user principal name (UPN) value.</span></span> <span data-ttu-id="53cbb-163">Vous pouvez modifier cette valeur sous l’onglet **Attribut**, comme illustré dans la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="53cbb-163">You can change this value on the **Attribute** tab, as shown in the following screenshot.</span></span> <span data-ttu-id="53cbb-164">L’intégration fonctionne uniquement une fois le mappage correctement terminé.</span><span class="sxs-lookup"><span data-stu-id="53cbb-164">The integration works only after you've completed the mapping correctly.</span></span>
    
    ![Boîte de dialogue Attributs de l’utilisateur](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_attribute.png)   

5. <span data-ttu-id="53cbb-166">Cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-166">Click **Save**.</span></span>

    ![Bouton Enregistrer de la fenêtre Configurer l’authentification unique](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_400.png)

6. <span data-ttu-id="53cbb-168">Pour ouvrir la fenêtre **Configurer l’authentification**, sous **Configuration d’IBM Kenexa Survey Enterprise**, cliquez sur **Configurer IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-168">To open the **Configure sign-on** window, under **IBM Kenexa Survey Enterprise Configuration**, click **Configure IBM Kenexa Survey Enterprise**.</span></span> 
 
    ![Lien Configurer IBM Kenexa Survey Enterprise](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_configure.png)

7. <span data-ttu-id="53cbb-170">Copiez les valeurs **URL de déconnexion**, **ID d’entité SAML** et **URL du service d’authentification unique SAML** à partir de la section **Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-170">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values from the **Quick Reference** section.</span></span>

8. <span data-ttu-id="53cbb-171">Dans la fenêtre **Configurer l’authentification**, sous **Référence rapide**, copiez les valeurs **URL de déconnexion**, **ID d’entité SAML** et **URL du service d’authentification unique SAML**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-171">In the **Configure sign-on** window, under **Quick Reference**, copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values.</span></span>

9. <span data-ttu-id="53cbb-172">Pour configurer l’authentification unique côté **IBM Kenexa Survey Enterprise**, envoyez les valeurs **Certificat (en base64)**, **URL de déconnexion**, **ID d’entité SAML** et **URL du service d’authentification unique SAML** téléchargées à l’[équipe de support technique IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="53cbb-172">To configure SSO on the **IBM Kenexa Survey Enterprise** side, send the downloaded **Certificate (Base64)**, **Sign-Out URL**, **SAML Entity ID**, and **SAML single sign-on Service URL** values to the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span>

> [!TIP]
> <span data-ttu-id="53cbb-173">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com) pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="53cbb-173">You can refer to a concise version of these instructions in the [Azure portal](https://portal.azure.com) while you are setting up the app.</span></span> <span data-ttu-id="53cbb-174">Après avoir ajouté cette application à partir de la section **Active Directory** > **Applications d’entreprise**, cliquez simplement sur l’onglet **Authentification unique** et accédez à la documentation incorporée par le biais de la section **Configuration** à la fin.</span><span class="sxs-lookup"><span data-stu-id="53cbb-174">After you add the app from the **Active Directory** > **Enterprise Applications** section, simply click the **single sign-on** tab, and then access the embedded documentation through the **Configuration** section at the end.</span></span> <span data-ttu-id="53cbb-175">Pour en savoir plus sur la fonctionnalité de documentation incorporée, consultez la [documentation incorporée d’Azure AD](https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="53cbb-175">To learn more about the embedded documentation feature, see [Azure AD embedded documentation](https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="53cbb-176">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="53cbb-176">Create an Azure AD test user</span></span>
<span data-ttu-id="53cbb-177">Dans cette section, vous allez créer un utilisateur de test nommé Britta Simon dans le portail Azure en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="53cbb-177">In this section, you create test user Britta Simon in the Azure portal by doing the following:</span></span>

![Créer un utilisateur de test Azure AD][100]

1. <span data-ttu-id="53cbb-179">Dans le volet gauche du Portail Azure, cliquez sur le bouton **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-179">In the Azure portal, in the left pane, click the **Azure Active Directory** button.</span></span>

    ![Bouton Azure Active Directory](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="53cbb-181">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis cliquez sur **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-181">To display the list of users, go to **Users and groups**, and then click **All users**.</span></span>
    
    ![Liens « Utilisateurs et groupes » et « Tous les utilisateurs »](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="53cbb-183">Pour ouvrir la boîte de dialogue **Utilisateur**, cliquez sur **Ajouter** en haut de la boîte de dialogue **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-183">To open the **User** dialog box, click **Add** at the top of the **All Users** dialog box.</span></span>
 
    ![Bouton Ajouter](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="53cbb-185">Dans la boîte de dialogue **Utilisateur**, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="53cbb-185">In the **User** dialog box, perform the following steps:</span></span>
 
    ![Boîte de dialogue Utilisateur](./media/active-directory-saas-kenexasurvey-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="53cbb-187">a.</span><span class="sxs-lookup"><span data-stu-id="53cbb-187">a.</span></span> <span data-ttu-id="53cbb-188">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-188">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="53cbb-189">b.</span><span class="sxs-lookup"><span data-stu-id="53cbb-189">b.</span></span> <span data-ttu-id="53cbb-190">Dans la zone **Nom d’utilisateur** , tapez l’adresse e-mail de l’utilisateur Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="53cbb-190">In the **User name** box, type the email address of user Britta Simon.</span></span>

    <span data-ttu-id="53cbb-191">c.</span><span class="sxs-lookup"><span data-stu-id="53cbb-191">c.</span></span> <span data-ttu-id="53cbb-192">Cochez la case **Afficher le mot de passe**, puis notez la valeur affichée dans le champ **Mot de passe**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-192">Select the **Show Password** check box, and then write down the value that's displayed in the **Password** box.</span></span>

    <span data-ttu-id="53cbb-193">d.</span><span class="sxs-lookup"><span data-stu-id="53cbb-193">d.</span></span> <span data-ttu-id="53cbb-194">Cliquez sur **Create**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-194">Click **Create**.</span></span>
 
### <a name="create-an-ibm-kenexa-survey-enterprise-test-user"></a><span data-ttu-id="53cbb-195">Créer un utilisateur de test IBM Kenexa Survey Enterprise</span><span class="sxs-lookup"><span data-stu-id="53cbb-195">Create an IBM Kenexa Survey Enterprise test user</span></span>

<span data-ttu-id="53cbb-196">Dans cette section, vous allez créer un utilisateur appelé Britta Simon dans IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="53cbb-196">In this section, you create a user called Britta Simon in IBM Kenexa Survey Enterprise.</span></span> 

<span data-ttu-id="53cbb-197">Pour créer des utilisateurs dans le système IBM Kenexa Survey Enterprise et mapper l’ID SSO pour ceux-ci, vous pouvez collaborer avec l’[équipe de support technique IBM Kenexa Survey Enterprise](https://www.ibm.com/support/home/?lnk=fcw).</span><span class="sxs-lookup"><span data-stu-id="53cbb-197">To create users in the IBM Kenexa Survey Enterprise system and map the SSO ID for them, you can work with the [IBM Kenexa Survey Enterprise support team](https://www.ibm.com/support/home/?lnk=fcw).</span></span> <span data-ttu-id="53cbb-198">Par ailleurs, cette ID SSO doit être mappé à la valeur d’identificateur d’utilisateur fournie par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="53cbb-198">This SSO ID value should also be mapped to the user identifier value from Azure AD.</span></span> <span data-ttu-id="53cbb-199">Vous pouvez modifier ce paramètre par défaut sous l’onglet **Attribut**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-199">You can change this default setting on the **Attribute** tab.</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="53cbb-200">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="53cbb-200">Assign the Azure AD test user</span></span>

<span data-ttu-id="53cbb-201">Dans cette section, vous allez autoriser l’utilisateur Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="53cbb-201">In this section, you enable user Britta Simon to use Azure SSO by granting access to IBM Kenexa Survey Enterprise.</span></span>

![Attribuer le rôle d’utilisateur][200] 

<span data-ttu-id="53cbb-203">Pour affecter l’utilisateur Britta Simon à IBM Kenexa Survey Enterprise, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="53cbb-203">To assign user Britta Simon to IBM Kenexa Survey Enterprise, do the following:</span></span>

1. <span data-ttu-id="53cbb-204">Dans le portail Azure, ouvrez la vue **Applications**, accédez à la vue **Répertoire**, sélectionnez **Applications d’entreprise**, puis cliquez sur **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-204">In the Azure portal, open the **Applications** view, go to the **Directory** view, select **Enterprise applications**, and then click **All applications**.</span></span>

    ![Liens « Applications d’entreprise » et « Toutes les applications »][201] 

2. <span data-ttu-id="53cbb-206">Dans la liste **Applications**, sélectionnez **IBM Kenexa Survey Enterprise**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-206">In the **Applications** list, select **IBM Kenexa Survey Enterprise**.</span></span>

    ![Lien IBM Kenexa Survey Enterprise dans la liste Applications](./media/active-directory-saas-kenexasurvey-tutorial/tutorial_kenexasurvey_app.png) 

3. <span data-ttu-id="53cbb-208">Dans le volet gauche, cliquez sur **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-208">In the left pane, click **Users and groups**.</span></span>

    ![Lien « Utilisateurs et groupes »][202] 

4. <span data-ttu-id="53cbb-210">Cliquez sur le bouton **Ajouter** puis, dans le volet **Ajouter une affectation**, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-210">Click the **Add** button and then, in the **Add Assignment** pane, select **Users and groups**.</span></span>

    ![Volet Ajouter une affectation][203]

5. <span data-ttu-id="53cbb-212">Dans la boîte de dialogue **Utilisateurs et groupes**, dans la liste **Utilisateurs**, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-212">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="53cbb-213">Dans la boîte de dialogue **Utilisateurs et groupes**, cliquez sur le bouton **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-213">In the **Users and groups** dialog box, click the **Select** button.</span></span>

7. <span data-ttu-id="53cbb-214">Dans la boîte de dialogue **Ajouter une attribution**, cliquez sur le bouton **Attribuer**.</span><span class="sxs-lookup"><span data-stu-id="53cbb-214">In the **Add Assignment** dialog box, click the **Assign** button.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="53cbb-215">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="53cbb-215">Test single sign-on</span></span>

<span data-ttu-id="53cbb-216">Dans cette section, vous allez tester la configuration SSO Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="53cbb-216">In this section, you test your Azure AD SSO configuration by using the Access Panel.</span></span>

<span data-ttu-id="53cbb-217">Lorsque vous cliquez sur la vignette **IBM Kenexa Survey Enterprise** dans le panneau d’accès, vous devez être connecté automatiquement à votre application IBM Kenexa Survey Enterprise.</span><span class="sxs-lookup"><span data-stu-id="53cbb-217">When you click the **IBM Kenexa Survey Enterprise** tile in the Access Panel, you should be automatically signed in to your IBM Kenexa Survey Enterprise application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="53cbb-218">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="53cbb-218">Additional resources</span></span>

* [<span data-ttu-id="53cbb-219">Liste de didacticiels sur l’intégration d’applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="53cbb-219">List of tutorials on how to integrate SaaS apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="53cbb-220">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="53cbb-220">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

<!--Image references-->

[1]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-kenexasurvey-tutorial/tutorial_general_203.png

 
