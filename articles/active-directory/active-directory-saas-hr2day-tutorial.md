---
title: "Didacticiel : Intégration d’Azure Active Directory avec HR2day by Merces | Microsoft Docs"
description: "Découvrez comment configurer l’authentification unique entre Azure Active Directory et HR2day by Merces."
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.assetid: 853d08c9-27b1-48d4-b8e7-3705140eb67f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/24/2017
ms.author: jeedes
ms.openlocfilehash: 77e2fcf9c306259286b15767f3a992510d6d79d8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-azure-active-directory-integration-with-hr2day-by-merces"></a><span data-ttu-id="4fddf-103">Didacticiel : Intégration d’Azure Active Directory avec HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="4fddf-103">Tutorial: Azure Active Directory integration with HR2day by Merces</span></span>

<span data-ttu-id="4fddf-104">Dans ce didacticiel, vous allez apprendre à intégrer HR2day by Merces à Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="4fddf-104">In this tutorial, you learn how to integrate HR2day by Merces with Azure Active Directory (Azure AD).</span></span>

<span data-ttu-id="4fddf-105">L’intégration de HR2day dans Azure AD vous offre les avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="4fddf-105">Integrating HR2day by Merces with Azure AD provides you with the following benefits:</span></span>

- <span data-ttu-id="4fddf-106">Dans Azure AD, vous pouvez contrôler qui a accès à HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="4fddf-106">You can control in Azure AD who has access to HR2day by Merces.</span></span>
- <span data-ttu-id="4fddf-107">Vous pouvez autoriser les utilisateurs à se connecter automatiquement à HR2day by Merces avec leur compte Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fddf-107">You can enable your users to automatically get signed in to HR2day by Merces with their Azure AD accounts.</span></span>
- <span data-ttu-id="4fddf-108">Vous pouvez gérer vos comptes à un emplacement central : le portail Azure</span><span class="sxs-lookup"><span data-stu-id="4fddf-108">You can manage your accounts in one central location--the Azure portal.</span></span>

<span data-ttu-id="4fddf-109">Pour en savoir plus sur l’intégration des applications SaaS avec Azure AD, consultez [Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?](active-directory-appssoaccess-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="4fddf-109">For more information about SaaS app integration with Azure AD, see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fddf-110">Composants requis</span><span class="sxs-lookup"><span data-stu-id="4fddf-110">Prerequisites</span></span>

<span data-ttu-id="4fddf-111">Pour configurer l’intégration d’Azure AD avec HR2day by Merces, vous avez besoin des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="4fddf-111">To configure Azure AD integration with HR2day by Merces, you need the following items:</span></span>

- <span data-ttu-id="4fddf-112">Un abonnement Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fddf-112">An Azure AD subscription.</span></span>
- <span data-ttu-id="4fddf-113">Un abonnement HR2day by Merces pour lequel l’authentification unique est activée</span><span class="sxs-lookup"><span data-stu-id="4fddf-113">An HR2day by Merces single sign-on enabled subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="4fddf-114">Nous déconseillons l’utilisation d’un environnement de production pour tester les étapes de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="4fddf-114">We don't recommend using a production environment to test the steps in this tutorial.</span></span>

<span data-ttu-id="4fddf-115">Pour tester la procédure de ce didacticiel, suivez les recommandations ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="4fddf-115">To test the steps in this tutorial, follow these recommendations:</span></span>

- <span data-ttu-id="4fddf-116">N’utilisez pas votre environnement de production, sauf si cela est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="4fddf-116">Don't use your production environment unless it's necessary.</span></span>
- <span data-ttu-id="4fddf-117">Obtenez [un mois d’évaluation gratuite d’Azure AD](https://azure.microsoft.com/pricing/free-trial/) si vous n’y avez pas encore accès.</span><span class="sxs-lookup"><span data-stu-id="4fddf-117">Get a [one-month free trial of Azure AD](https://azure.microsoft.com/pricing/free-trial/) if you don't already have it.</span></span>  

## <a name="scenario-description"></a><span data-ttu-id="4fddf-118">Description du scénario</span><span class="sxs-lookup"><span data-stu-id="4fddf-118">Scenario description</span></span>
<span data-ttu-id="4fddf-119">Dans ce didacticiel, vous testez l’authentification unique Azure AD dans un environnement de test.</span><span class="sxs-lookup"><span data-stu-id="4fddf-119">In this tutorial, you test Azure AD single sign-on in a test environment.</span></span> <span data-ttu-id="4fddf-120">Le scénario décrit dans ici se compose des deux sections principales suivantes :</span><span class="sxs-lookup"><span data-stu-id="4fddf-120">The scenario that's outlined here consists of two main building blocks:</span></span>

1. <span data-ttu-id="4fddf-121">Ajout de HR2day by Merces à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="4fddf-121">Adding HR2day by Merces from the gallery.</span></span>
2. <span data-ttu-id="4fddf-122">Configuration et test de l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fddf-122">Configuring and testing Azure AD single sign-on.</span></span>

## <a name="add-hr2day-by-merces-from-the-gallery"></a><span data-ttu-id="4fddf-123">Ajouter HR2day by Merces à partir de la galerie</span><span class="sxs-lookup"><span data-stu-id="4fddf-123">Add HR2day by Merces from the gallery</span></span>
<span data-ttu-id="4fddf-124">Pour configurer l’intégration de HR2day by Merces avec Azure AD, vous devez ajouter HR2day by Merces à partir de la galerie à votre liste d’applications SaaS gérées.</span><span class="sxs-lookup"><span data-stu-id="4fddf-124">To configure the integration of HR2day by Merces into Azure AD, add HR2day by Merces from the gallery to your list of managed SaaS apps.</span></span>

<span data-ttu-id="4fddf-125">**Pour ajouter HR2day by Merces à partir de la galerie, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="4fddf-125">**To add HR2day by Merces from the gallery, take the following steps:**</span></span>

1. <span data-ttu-id="4fddf-126">Dans le panneau de navigation de gauche du [portail Azure](https://portal.azure.com), cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-126">In the [Azure portal](https://portal.azure.com), on the left navigation pane, select the **Azure Active Directory** icon.</span></span> 

    ![Active Directory][1]

2. <span data-ttu-id="4fddf-128">Accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-128">Go to **Enterprise applications**.</span></span> <span data-ttu-id="4fddf-129">Accédez ensuite à **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-129">Then go to **All applications**.</span></span>

    ![Applications][2]
    
3. <span data-ttu-id="4fddf-131">Pour ajouter une nouvelle application, cliquez sur le bouton **Nouvelle application** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4fddf-131">To add a new application, select the **New application** button on the top of the dialog box.</span></span>

    ![Applications][3]

4. <span data-ttu-id="4fddf-133">Dans la zone de recherche, tapez **HR2day by Merces**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-133">In the search box, type **HR2day by Merces**.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_search.png)

5. <span data-ttu-id="4fddf-135">Dans le panneau de résultats, sélectionnez **HR2day by Merces**, puis sélectionnez le bouton **Ajouter** pour ajouter l’application.</span><span class="sxs-lookup"><span data-stu-id="4fddf-135">In the results panel, select **HR2day by Merces**, and then select the **Add** button to add the application.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a><span data-ttu-id="4fddf-137">Configurer et tester l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fddf-137">Configure and test Azure AD single sign-on</span></span>
<span data-ttu-id="4fddf-138">Dans cette section, vous allez configurer et tester l’authentification unique Azure AD avec HR2day by Merces avec un utilisateur de test appelé « Britta Simon ».</span><span class="sxs-lookup"><span data-stu-id="4fddf-138">In this section, you configure and test Azure AD single sign-on with HR2day by Merces based on a test user called "Britta Simon."</span></span>

<span data-ttu-id="4fddf-139">Pour que l’authentification unique fonctionne, Azure AD doit savoir qui est l’utilisateur HR2day by Merces équivalent dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fddf-139">For single sign-on to work, Azure AD needs to know who the counterpart user in HR2day by Merces is to a user in Azure AD.</span></span> <span data-ttu-id="4fddf-140">En d’autres termes, vous devez établir un lien entre un utilisateur Azure AD et l’utilisateur HR2day by Merces associé.</span><span class="sxs-lookup"><span data-stu-id="4fddf-140">In other words, you need to establish a link between an Azure AD user and the related user in HR2day by Merces.</span></span>

<span data-ttu-id="4fddf-141">Dans HR2day by Merces, affectez le **nom d’utilisateur** dans Azure AD comme **Username** pour établir la relation.</span><span class="sxs-lookup"><span data-stu-id="4fddf-141">In HR2day by Merces, assign the **user name** in Azure AD to  **Username** to establish the relationship.</span></span>

<span data-ttu-id="4fddf-142">Pour configurer et tester l’authentification unique Azure AD avec HR2day by Merces, vous devez suivre les indications des sections suivantes :</span><span class="sxs-lookup"><span data-stu-id="4fddf-142">To configure and test Azure AD single sign-on with HR2day by Merces, you need to complete the following building blocks:</span></span>

1. <span data-ttu-id="4fddf-143">[Configurer l’authentification unique Azure AD](#configuring-azure-ad-single-sign-on) : Permettre à vos utilisateurs d’utiliser cette fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="4fddf-143">[Configure Azure AD single sign-on](#configuring-azure-ad-single-sign-on): Enable your users to use this feature.</span></span>
2. <span data-ttu-id="4fddf-144">[Créer un utilisateur de test Azure AD](#creating-an-azure-ad-test-user) : Tester l’authentification unique Azure AD avec Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fddf-144">[Create an Azure AD test user](#creating-an-azure-ad-test-user): Test Azure AD single sign-on with Britta Simon.</span></span>
3. <span data-ttu-id="4fddf-145">[Créer un utilisateur test HR2day by Merces](#creating-an-hr2day-by-merces-test-user) : Créer un équivalent de Britta Simon dans HR2day by Merces lié à la représentation de l’utilisateur Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fddf-145">[Create an HR2day by Merces test user](#creating-an-hr2day-by-merces-test-user): Create a counterpart of Britta Simon in HR2day by Merces that is linked to the Azure AD representation of user.</span></span>
4. <span data-ttu-id="4fddf-146">[Affecter l’utilisateur de test Azure AD](#assigning-the-azure-ad-test-user) : Permettre à Britta Simon d’utiliser l’authentification unique Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fddf-146">[Assign the Azure AD test user](#assigning-the-azure-ad-test-user): Enable Britta Simon to use Azure AD single sign-on.</span></span>
5. <span data-ttu-id="4fddf-147">[Tester l’authentification unique](#testing-single-sign-on) : Vérifier si la configuration fonctionne.</span><span class="sxs-lookup"><span data-stu-id="4fddf-147">[Test single sign-on](#testing-single-sign-on): Verify whether the configuration works.</span></span>

### <a name="configure-azure-ad-single-sign-on"></a><span data-ttu-id="4fddf-148">Configurer l’authentification unique Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fddf-148">Configure Azure AD single sign-on</span></span>

<span data-ttu-id="4fddf-149">Dans cette section, vous allez activer l’authentification unique Azure AD dans le portail Azure et configurer l’authentification unique dans votre application HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="4fddf-149">In this section, you enable Azure AD single sign-on in the Azure portal and configure single sign-on in your HR2day by Merces application.</span></span>

<span data-ttu-id="4fddf-150">**Pour configurer l’authentification unique Azure AD avec HR2day by Merces, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="4fddf-150">**To configure Azure AD single sign-on with HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="4fddf-151">Dans le Portail Azure, dans la page d’intégration de l’application **HR2day by Merces**, sélectionnez **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-151">In the Azure portal, on the **HR2day by Merces** application integration page, select **Single sign-on**.</span></span>

    ![Configurer l’authentification unique][4]

2. <span data-ttu-id="4fddf-153">Pour activer l’authentification unique, dans la boîte de dialogue **Authentification unique**, sélectionnez **Mode** comme **Authentification basée sur SAML**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-153">To enable single sign-on, in the **Single sign-on** dialog box, select **Mode** as **SAML-based Sign-on**.</span></span>
 
    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_samlbase.png)

3. <span data-ttu-id="4fddf-155">Dans la section **Domaine et URL HR2day by Merces**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4fddf-155">In the **HR2day by Merces Domain and URLs** section, take the following steps:</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_url.png)

    <span data-ttu-id="4fddf-157">a.</span><span class="sxs-lookup"><span data-stu-id="4fddf-157">a.</span></span> <span data-ttu-id="4fddf-158">Dans la zone **URL de connexion**, tapez une URL au format suivant : `https://<tenantname>.force.com/<instancename>`.</span><span class="sxs-lookup"><span data-stu-id="4fddf-158">In the **Sign-on URL** box, type a URL by using the following pattern: `https://<tenantname>.force.com/<instancename>`.</span></span>

    <span data-ttu-id="4fddf-159">b.</span><span class="sxs-lookup"><span data-stu-id="4fddf-159">b.</span></span> <span data-ttu-id="4fddf-160">Dans la zone de texte **Identificateur**, tapez une URL au format suivant : `https://hr2day.force.com/<companyname>`.</span><span class="sxs-lookup"><span data-stu-id="4fddf-160">In the **Identifier** box, type a URL by using the following pattern: `https://hr2day.force.com/<companyname>`.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="4fddf-161">Il ne s’agit pas de valeurs réelles.</span><span class="sxs-lookup"><span data-stu-id="4fddf-161">These values are not real.</span></span> <span data-ttu-id="4fddf-162">Mettez à jour ces valeurs avec l’URL de connexion et l’identificateur réels.</span><span class="sxs-lookup"><span data-stu-id="4fddf-162">Update these values with the actual sign-on URL and identifier.</span></span> <span data-ttu-id="4fddf-163">Pour obtenir ces valeurs, contactez l’[équipe du support client HR2day by Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="4fddf-163">Contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl) to get these values.</span></span> 
 


4. <span data-ttu-id="4fddf-164">Dans la section **Certificat de signature SAML**, sélectionnez **Téléchargez le certificat (Base64)** puis enregistrez le fichier du certificat sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="4fddf-164">On the **SAML Signing Certificate** section, select **Certificate(Base64)**, and then save the certificate file on your computer.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_certificate.png) 

5. <span data-ttu-id="4fddf-166">Cette section décrit comment permettre aux utilisateurs de s’authentifier sur HR2day by Merces avec leur compte Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4fddf-166">This section describes how to enable users to authenticate to HR2day by Merces with their account in Azure AD.</span></span> <span data-ttu-id="4fddf-167">Pour cela, ils utilisent la fédération basée sur le protocole SAML.</span><span class="sxs-lookup"><span data-stu-id="4fddf-167">They do this by using federation that's based on the SAML protocol.</span></span>

    <span data-ttu-id="4fddf-168">Votre application HR2day by Merces attend les assertions SAML dans un format spécifique, ce qui vous oblige à ajouter des mappages d’attributs personnalisés à votre jeton SAML.</span><span class="sxs-lookup"><span data-stu-id="4fddf-168">Your HR2day by Merces application expects the SAML assertions in a specific format, which requires you to add custom attribute mappings to your SAML token.</span></span> <span data-ttu-id="4fddf-169">La capture d’écran suivante présente un exemple de cette opération.</span><span class="sxs-lookup"><span data-stu-id="4fddf-169">The following screenshot shows an example of this.</span></span> 

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2day_00.png)
    
    > [!NOTE] 
    <span data-ttu-id="4fddf-171">Avant de pouvoir configurer votre assertion SAML, vous devez contacter [l’équipe du support client HR2day by Merces](mailto:servicedesk@merces.nl) et lui demander d’affecter la valeur d’attribut d’identificateur unique à votre locataire.</span><span class="sxs-lookup"><span data-stu-id="4fddf-171">Before you can configure the SAML assertion, you must contact the [HR2day by Merces Client support team](mailto:servicedesk@merces.nl) and request the value of the unique identifier attribute for your tenant.</span></span> <span data-ttu-id="4fddf-172">Vous avez besoin de cette valeur pour exécuter les étapes de la section suivante.</span><span class="sxs-lookup"><span data-stu-id="4fddf-172">You need this value to complete the steps in the next section.</span></span> 

6. <span data-ttu-id="4fddf-173">Dans la boîte de dialogue **Authentification unique**, dans la section **Attributs utilisateur**, configurez l’attribut de jeton SAML comme illustré ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="4fddf-173">In the **Single sign-on** dialog box, in the **User Attributes** section, configure the SAML token attribute as shown in the following image.</span></span> <span data-ttu-id="4fddf-174">Ensuite, effectuez les étapes suivantes.</span><span class="sxs-lookup"><span data-stu-id="4fddf-174">Then take the following steps.</span></span>
    
      | <span data-ttu-id="4fddf-175">Nom de l’attribut</span><span class="sxs-lookup"><span data-stu-id="4fddf-175">Attribute name</span></span>    |   <span data-ttu-id="4fddf-176">Valeur de l’attribut</span><span class="sxs-lookup"><span data-stu-id="4fddf-176">Attribute value</span></span> |  
    | ------------------- | -------------------- |    
    | <span data-ttu-id="4fddf-177">ATTR_LOGINCLAIM</span><span class="sxs-lookup"><span data-stu-id="4fddf-177">ATTR_LOGINCLAIM</span></span> | <span data-ttu-id="4fddf-178">join([mail],"102938475Z","@"</span><span class="sxs-lookup"><span data-stu-id="4fddf-178">join([mail],"102938475Z","@"</span></span> |
    
      <span data-ttu-id="4fddf-179">a.</span><span class="sxs-lookup"><span data-stu-id="4fddf-179">a.</span></span> <span data-ttu-id="4fddf-180">Pour ouvrir la boîte de dialogue **Ajouter un attribut**, cliquez sur **Ajouter un attribut**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-180">To open the **Add Attribute** dialog, select **Add attribute**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_04.png)

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_attribute_05.png)

    <span data-ttu-id="4fddf-183">b.</span><span class="sxs-lookup"><span data-stu-id="4fddf-183">b.</span></span> <span data-ttu-id="4fddf-184">Dans la zone de texte **Nom**, tapez **ATTR_LOGINCLAIM**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-184">In the **Name** box, type **ATTR_LOGINCLAIM**.</span></span>

    <span data-ttu-id="4fddf-185">c.</span><span class="sxs-lookup"><span data-stu-id="4fddf-185">c.</span></span> <span data-ttu-id="4fddf-186">Dans la liste **Valeur**, sélectionnez **Join()**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-186">From the **Value** list, select **Join()**.</span></span>

    <span data-ttu-id="4fddf-187">d.</span><span class="sxs-lookup"><span data-stu-id="4fddf-187">d.</span></span> <span data-ttu-id="4fddf-188">Dans la liste **String1**, sélectionnez **User.mail**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-188">From the **String1** list, select **user.mail**.</span></span>

    <span data-ttu-id="4fddf-189">e.</span><span class="sxs-lookup"><span data-stu-id="4fddf-189">e.</span></span> <span data-ttu-id="4fddf-190">Dans **String2**, tapez l’identificateur unique fourni par votre équipe HR2day.</span><span class="sxs-lookup"><span data-stu-id="4fddf-190">For **String2**, type the unique identifier that's provided by your HR2day team.</span></span>

    <span data-ttu-id="4fddf-191">f.</span><span class="sxs-lookup"><span data-stu-id="4fddf-191">f.</span></span> <span data-ttu-id="4fddf-192">Dans la zone **Séparateur**, tapez **@**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-192">In the **Separator** box, type **@**.</span></span>
    
    <span data-ttu-id="4fddf-193">g.</span><span class="sxs-lookup"><span data-stu-id="4fddf-193">g.</span></span> <span data-ttu-id="4fddf-194">Sélectionnez **OK**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-194">Select **Ok**.</span></span>

7. <span data-ttu-id="4fddf-195">Sélectionnez le bouton **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-195">Select the **Save** button.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_general_400.png)

8. <span data-ttu-id="4fddf-197">Dans la section**Configuration de HR2day by Merces**, sélectionnez **Configurer HR2day by Merces** pour ouvrir la fenêtre **Configurer l’authentification**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-197">In the **HR2day by Merces Configuration** section, select **Configure HR2day by Merces** to open the **Configure sign-on** window.</span></span> <span data-ttu-id="4fddf-198">Copiez l’**URL de déconnexion**, l’**ID d’entité SAML** et l’**URL du service d’authentification unique SAML** à partir de la section **Référence rapide**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-198">Copy the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** from the **Quick Reference** section.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_configure.png) 

9. <span data-ttu-id="4fddf-200">Pour configurer l’authentification unique pour votre application, contactez l’[équipe du support client HR2day by Merces](mailTo:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="4fddf-200">To configure SSO  for your application, contact the [HR2day by Merces client support team](mailTo:servicedesk@merces.nl).</span></span> <span data-ttu-id="4fddf-201">Joignez le fichier **Certificat (Base64)** téléchargé à votre e-mail.</span><span class="sxs-lookup"><span data-stu-id="4fddf-201">Attach the downloaded **Certificate(Base64)** file to your email.</span></span> <span data-ttu-id="4fddf-202">Indiquez également l’**URL de déconnexion**, l’**ID de l’entité SAML** et l’**URL du service d’authentification unique SAML**, afin de pouvoir les configurer pour l’intégration de l’authentification unique.</span><span class="sxs-lookup"><span data-stu-id="4fddf-202">Also provide the **Sign-Out URL**, **SAML Entity ID**, and **SAML Single Sign-On Service URL** so that they can be configured for SSO integration.</span></span>

    > [!NOTE]
    ><span data-ttu-id="4fddf-203">N’oubliez pas d’indiquer à l’équipe de Merces que cette intégration nécessite la définition de l’ID d’entité en suivant le modèle **https://hr2day.force.com/NOM_INSTANCE**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-203">Mention to the Merces team that this integration needs the Entity ID to be set with the pattern **https://hr2day.force.com/INSTANCENAME**.</span></span>

    > [!TIP]
    ><span data-ttu-id="4fddf-204">Vous pouvez maintenant lire une version concise de ces instructions dans le [portail Azure](https://portal.azure.com), pendant que vous configurez l’application.</span><span class="sxs-lookup"><span data-stu-id="4fddf-204">You can now read a concise version of these instructions inside the [Azure portal](https://portal.azure.com), while you are setting up the app!</span></span>  <span data-ttu-id="4fddf-205">Après avoir ajouté cette application à partir de la section **Active Directory** > **Applications d’entreprise**, sélectionnez l’onglet **Authentification unique**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-205">After you add this app from the **Active Directory** > **Enterprise Applications** section, select the **Single Sign-On** tab.</span></span> <span data-ttu-id="4fddf-206">Ensuite, accédez à la documentation incorporée par le biais de la section **Configuration** en bas.</span><span class="sxs-lookup"><span data-stu-id="4fddf-206">Then access the embedded documentation through the **Configuration** section at the bottom.</span></span> <span data-ttu-id="4fddf-207">Pour en savoir plus sur la fonctionnalité de documentation incorporée, consultez [Documentation incorporée Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985).</span><span class="sxs-lookup"><span data-stu-id="4fddf-207">You can read more about the embedded documentation feature in the [Azure AD embedded documentation]( https://go.microsoft.com/fwlink/?linkid=845985).</span></span>
> 

### <a name="create-an-azure-ad-test-user"></a><span data-ttu-id="4fddf-208">Créer un utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fddf-208">Create an Azure AD test user</span></span>
<span data-ttu-id="4fddf-209">L’objectif de cette section est de créer un utilisateur de test appelé Britta Simon dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="4fddf-209">The objective of this section is to create a test user in the Azure portal called Britta Simon.</span></span>

![Créer un utilisateur Azure AD][100]

<span data-ttu-id="4fddf-211">**Pour créer un utilisateur de test dans Azure AD, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="4fddf-211">**To create a test user in Azure AD, take the following steps:**</span></span>

1. <span data-ttu-id="4fddf-212">Dans le panneau de navigation de gauche du **portail Azure**, cliquez sur l’icône **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-212">In the **Azure portal**, on the left navigation pane, select the **Azure Active Directory** icon.</span></span>

    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_01.png) 

2. <span data-ttu-id="4fddf-214">Pour afficher la liste des utilisateurs, accédez à **Utilisateurs et groupes**, puis sélectionnez **Tous les utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-214">To display the list of users, go to **Users and groups**, and then select **All users**.</span></span>
    
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_02.png) 

3. <span data-ttu-id="4fddf-216">Pour ouvrir la boîte de dialogue **Utilisateur**, sélectionnez **Ajouter** en haut de la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="4fddf-216">To open the **User** dialog box, select **Add** on the top of the dialog box.</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_03.png) 

4. <span data-ttu-id="4fddf-218">Dans la boîte de dialogue **Utilisateur**, effectuez les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="4fddf-218">In the **User** dialog box, take the following steps:</span></span>
 
    ![Création d’un utilisateur de test Azure AD](./media/active-directory-saas-hr2day-tutorial/create_aaduser_04.png) 

    <span data-ttu-id="4fddf-220">a.</span><span class="sxs-lookup"><span data-stu-id="4fddf-220">a.</span></span> <span data-ttu-id="4fddf-221">Dans la zone **Nom**, tapez **BrittaSimon**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-221">In the **Name** box, type **BrittaSimon**.</span></span>

    <span data-ttu-id="4fddf-222">b.</span><span class="sxs-lookup"><span data-stu-id="4fddf-222">b.</span></span> <span data-ttu-id="4fddf-223">Dans la zone **Nom d’utilisateur**, tapez l’**adresse e-mail** de Britta Simon.</span><span class="sxs-lookup"><span data-stu-id="4fddf-223">In the **User name** box, type the **email address** of BrittaSimon.</span></span>

    <span data-ttu-id="4fddf-224">c.</span><span class="sxs-lookup"><span data-stu-id="4fddf-224">c.</span></span> <span data-ttu-id="4fddf-225">Sélectionnez **Afficher le mot de passe** et notez le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="4fddf-225">Select **Show Password**, and then write down the password.</span></span>

    <span data-ttu-id="4fddf-226">d.</span><span class="sxs-lookup"><span data-stu-id="4fddf-226">d.</span></span> <span data-ttu-id="4fddf-227">Sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-227">Select **Create**.</span></span>
 
### <a name="create-an-hr2day-by-merces-test-user"></a><span data-ttu-id="4fddf-228">Créer un utilisateur test HR2day by Merces</span><span class="sxs-lookup"><span data-stu-id="4fddf-228">Create an HR2day by Merces test user</span></span>

<span data-ttu-id="4fddf-229">L’objectif de cette section est de créer un utilisateur appelé Britta Simon dans HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="4fddf-229">The objective of this section is to create a user called Britta Simon in HR2day by Merces.</span></span> <span data-ttu-id="4fddf-230">Pour ajouter des utilisateurs dans le compte HR2day, collaborez avec l’[équipe du support client HR2day by Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="4fddf-230">To add the users in the HR2day account, work with the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span> 

> [!NOTE]
> <span data-ttu-id="4fddf-231">Si vous devez créer un utilisateur manuellement, contactez l’[équipe du support client HR2day by Merces](mailto:servicedesk@merces.nl).</span><span class="sxs-lookup"><span data-stu-id="4fddf-231">If you need to create a user manually, contact the [HR2day by Merces client support team](mailto:servicedesk@merces.nl).</span></span>

### <a name="assign-the-azure-ad-test-user"></a><span data-ttu-id="4fddf-232">Affecter l’utilisateur de test Azure AD</span><span class="sxs-lookup"><span data-stu-id="4fddf-232">Assign the Azure AD test user</span></span>

<span data-ttu-id="4fddf-233">Dans cette section, vous allez autoriser Britta Simon à utiliser l’authentification unique Azure en lui accordant l’accès à HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="4fddf-233">In this section, you enable Britta Simon to use Azure single sign-on by granting her access to HR2day by Merces.</span></span>

![Affecter des utilisateurs][200] 

<span data-ttu-id="4fddf-235">**Pour affecter Britta Simon à HR2day by Merces, effectuez les étapes suivantes :**</span><span class="sxs-lookup"><span data-stu-id="4fddf-235">**To assign Britta Simon to HR2day by Merces, take the following steps:**</span></span>

1. <span data-ttu-id="4fddf-236">Dans le portail Azure, ouvrez la vue des applications, accédez à la vue des répertoires, puis accédez à **Applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-236">In the Azure portal, open the applications view, go to the directory view, and then go to **Enterprise applications**.</span></span> <span data-ttu-id="4fddf-237">Ensuite, sélectionnez **Toutes les applications**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-237">Next, select **All applications**.</span></span>

    ![Affecter des utilisateurs][201] 

2. <span data-ttu-id="4fddf-239">Dans la liste des applications, sélectionnez **HR2day by Merces**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-239">In the applications list, select **HR2day by Merces**.</span></span>

    ![Configurer l’authentification unique](./media/active-directory-saas-hr2day-tutorial/tutorial_hr2daybymerces_app.png) 

3. <span data-ttu-id="4fddf-241">Dans le menu de gauche, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-241">In the menu on the left, select **Users and groups**.</span></span>

    ![Affecter des utilisateurs][202] 

4. <span data-ttu-id="4fddf-243">Sélectionnez le bouton **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-243">Select the **Add** button.</span></span> <span data-ttu-id="4fddf-244">Ensuite, dans la boîte de dialogue **Ajouter une attribution**, sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-244">Then, in the **Add Assignment** dialog box, select **Users and groups**.</span></span>

    ![Affecter des utilisateurs][203]

5. <span data-ttu-id="4fddf-246">Dans la boîte de dialogue **Utilisateurs et groupes**, dans la liste **Utilisateurs**, sélectionnez **Britta Simon**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-246">In the **Users and groups** dialog box, in the **Users** list, select **Britta Simon**.</span></span>

6. <span data-ttu-id="4fddf-247">Cliquez sur le bouton **Sélectionner**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-247">Click the **Select** button.</span></span>

7. <span data-ttu-id="4fddf-248">Dans la boîte de dialogue **Ajouter une attribution**, sélectionnez **Affecter**.</span><span class="sxs-lookup"><span data-stu-id="4fddf-248">In the **Add Assignment** dialog box, select **Assign**.</span></span>
    
### <a name="test-single-sign-on"></a><span data-ttu-id="4fddf-249">Tester l’authentification unique</span><span class="sxs-lookup"><span data-stu-id="4fddf-249">Test single sign-on</span></span>

<span data-ttu-id="4fddf-250">L’objectif de cette section est de tester la configuration de l’authentification unique Azure AD à l’aide du volet d’accès.</span><span class="sxs-lookup"><span data-stu-id="4fddf-250">The objective of this section is to test your Azure AD single sign-on configuration by using the Access Panel.</span></span>  

<span data-ttu-id="4fddf-251">Quand vous sélectionnez la vignette HR2day by Merces dans le volet d’accès, vous êtes connecté automatiquement à votre application HR2day by Merces.</span><span class="sxs-lookup"><span data-stu-id="4fddf-251">When you select the HR2day by Merces tile in the Access Panel, you automatically get signed in  to your HR2day by Merces application.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="4fddf-252">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4fddf-252">Additional resources</span></span>

* [<span data-ttu-id="4fddf-253">Liste de didacticiels sur les procédures d’intégration des applications SaaS avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4fddf-253">List of tutorials about how to Integrate SaaS Apps with Azure Active Directory</span></span>](active-directory-saas-tutorial-list.md)
* [<span data-ttu-id="4fddf-254">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4fddf-254">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)



<!--Image references-->

[1]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_01.png
[2]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_02.png
[3]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_03.png
[4]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_04.png

[100]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_100.png

[200]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_200.png
[201]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_201.png
[202]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_202.png
[203]: ./media/active-directory-saas-hr2day-tutorial/tutorial_general_203.png

