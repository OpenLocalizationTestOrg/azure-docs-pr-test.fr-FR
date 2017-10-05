---
title: "Azure Active Directory B2C : Ajout d’ADFS en tant que fournisseur d’identités SAML à l’aide de stratégies personnalisées"
description: "Un guide pratique sur la configuration d’ADFS 2016 à l’aide du protocole SAML et de stratégies personnalisées"
services: active-directory-b2c
documentationcenter: 
author: yoelhor
manager: joroja
editor: 
ms.assetid: 
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 08/04/2017
ms.author: yoelh
ms.openlocfilehash: ef0495460b5652dd6052a49ab9c722381e93458b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-b2c-add-adfs-as-a-saml-identity-provider-using-custom-policies"></a><span data-ttu-id="ca936-103">Azure Active Directory B2C : Ajout d’ADFS en tant que fournisseur d’identités SAML à l’aide de stratégies personnalisées</span><span class="sxs-lookup"><span data-stu-id="ca936-103">Azure Active Directory B2C: Add ADFS as a SAML identity provider using custom policies</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="ca936-104">Cet article vous montre comment activer l’identification pour les utilisateurs de comptes ADFS à l’aide des [stratégies personnalisées](active-directory-b2c-overview-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ca936-104">This article shows you how to enable sign-in for users from ADFS account through the use of [custom policies](active-directory-b2c-overview-custom.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca936-105">Composants requis</span><span class="sxs-lookup"><span data-stu-id="ca936-105">Prerequisites</span></span>

<span data-ttu-id="ca936-106">Suivez les étapes décrites dans [Bien démarrer avec les stratégies personnalisées](active-directory-b2c-get-started-custom.md).</span><span class="sxs-lookup"><span data-stu-id="ca936-106">Complete the steps in the [Getting started with custom policies](active-directory-b2c-get-started-custom.md) article.</span></span>

<span data-ttu-id="ca936-107">Ces étapes sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="ca936-107">These steps include:</span></span>

1.  <span data-ttu-id="ca936-108">Création d’une approbation de partie de confiance ADFS.</span><span class="sxs-lookup"><span data-stu-id="ca936-108">Creating an ADFS Relying Party Trust.</span></span>
2.  <span data-ttu-id="ca936-109">Ajout du certificat d’approbation de partie de confiance ADFS à Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ca936-109">Adding the ADFS Relying Party Trust certificate to Azure AD B2C.</span></span>
3.  <span data-ttu-id="ca936-110">Ajout du fournisseur de revendications à une stratégie.</span><span class="sxs-lookup"><span data-stu-id="ca936-110">Adding claims provider to a policy.</span></span>
4.  <span data-ttu-id="ca936-111">Inscription du fournisseur de revendications de compte ADFS à un parcours utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ca936-111">Registering the ADFS account claims provider to a user journey.</span></span>
5.  <span data-ttu-id="ca936-112">Téléchargement et test de la stratégie sur un client Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ca936-112">Uploading the policy to an Azure AD B2C tenant and test it.</span></span>

## <a name="to-create-a-claims-aware-relying-party-trust"></a><span data-ttu-id="ca936-113">Créer une approbation de partie de confiance prenant en charge les revendications</span><span class="sxs-lookup"><span data-stu-id="ca936-113">To create a claims-aware Relying Party Trust</span></span>

<span data-ttu-id="ca936-114">Pour utiliser ADFS en tant que fournisseur d’identité dans Azure Active Directory (Azure AD) B2C, vous devez créer une approbation de partie de confiance ADFS et lui fournir les paramètres appropriés.</span><span class="sxs-lookup"><span data-stu-id="ca936-114">To use ADFS as an identity provider in Azure Active Directory (Azure AD) B2C, you need to create an ADFS Relying Party Trust and supply it with the right parameters.</span></span>

<span data-ttu-id="ca936-115">Pour ajouter une nouvelle approbation de partie de confiance en utilisant le composant logiciel enfichable de gestion ADFS et configurer manuellement les paramètres, effectuez la procédure suivante sur un serveur de fédération.</span><span class="sxs-lookup"><span data-stu-id="ca936-115">To add a new relying party trust by using the AD FS Management snap-in and manually configure the settings, perform the following procedure on a federation server.</span></span>

<span data-ttu-id="ca936-116">L’appartenance au groupe **Administrateurs** ou équivalent sur l’ordinateur local est la condition minimale requise pour effectuer cette procédure.</span><span class="sxs-lookup"><span data-stu-id="ca936-116">Membership in **Administrators**, or equivalent, on the local computer is the minimum required to complete this procedure.</span></span> <span data-ttu-id="ca936-117">Examinez les informations relatives à l’utilisation des comptes et appartenances de groupe appropriés sur les [Groupes de domaine et locaux par défaut](http://go.microsoft.com/fwlink/?LinkId=83477)</span><span class="sxs-lookup"><span data-stu-id="ca936-117">Review details about using the appropriate accounts and group memberships at [Local and Domain Default Groups](http://go.microsoft.com/fwlink/?LinkId=83477)</span></span>

1.  <span data-ttu-id="ca936-118">Dans Gestionnaire de serveur, cliquez sur **Outils**, puis sélectionnez sur **Gestion ADFS**.</span><span class="sxs-lookup"><span data-stu-id="ca936-118">In Server Manager, click **Tools**, and then select **ADFS Management**.</span></span>

2.  <span data-ttu-id="ca936-119">Cliquez sur **Ajouter une approbation de partie de confiance**.</span><span class="sxs-lookup"><span data-stu-id="ca936-119">Click on **Add Relying Party Trust**.</span></span>
    <span data-ttu-id="ca936-120">![Ajouter une approbation de partie de confiance](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-120">![Add Relying Party Trust](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-1.png)</span></span>

3.  <span data-ttu-id="ca936-121">Sur la page **Bienvenue**, choisissez **Prise en charge des revendications** et cliquez sur **Démarrer**.</span><span class="sxs-lookup"><span data-stu-id="ca936-121">On the **Welcome** page, choose **Claims aware** and click **Start**.</span></span>
    <span data-ttu-id="ca936-122">![Sur la page d’accueil, choisissez Prise en charge des revendications](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-122">![On the Welcome page, choose Claims aware](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-2.png)</span></span>
4.  <span data-ttu-id="ca936-123">Sur la page **Sélectionner une source de données**, cliquez sur **Entrer manuellement les données relatives à la partie de confiance**, puis sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ca936-123">On the **Select Data Source** page, click **Enter data about the relying party manually**, and then click **Next**.</span></span>
    <span data-ttu-id="ca936-124">![Entrer les informations sur la partie de confiance](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-124">![Enter data about the relying party](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-3.png)</span></span>

5.  <span data-ttu-id="ca936-125">Sur la page **Spécifier le nom d’affichage**, saisissez un nom dans **Nom d’affichage**. Sous **Notes**, saisissez une description pour cette partie de confiance, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ca936-125">On the **Specify Display Name** page, type a name in **Display name**, under **Notes** type a description for this relying party trust, and then click **Next**.</span></span>
    <span data-ttu-id="ca936-126">![Spécifier le nom d’affichage et les notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-126">![Specify Display Name and notes](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-4.png)</span></span>
6.  <span data-ttu-id="ca936-127">facultatif.</span><span class="sxs-lookup"><span data-stu-id="ca936-127">Optional.</span></span> <span data-ttu-id="ca936-128">Si vous disposez d’un certificat de chiffrement de jeton facultatif, allez sur la page **Configurer certificat**, cliquez sur **Parcourir** pour localiser votre fichier de certificat, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ca936-128">If you have an optional token encryption certificate, then on the **Configure Certificate** page, click **Browse** to locate your certificate file, and then click **Next**.</span></span>
    <span data-ttu-id="ca936-129">![Configurer le certificat](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-129">![Configure Certificate](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-5.png)</span></span>
7.  <span data-ttu-id="ca936-130">Sur la page **Configurer l’URL**, cochez la case **Activer la prise en charge du protocole WebSSO SAML 2.0**.</span><span class="sxs-lookup"><span data-stu-id="ca936-130">On the **Configure URL** page, select the **Enable support for the SAML 2.0 WebSSO protocol** check box.</span></span> <span data-ttu-id="ca936-131">Sous **URL du service SSO SAML 2.0 de la partie de confiance**, saisissez l’URL du point de terminaison de service Security Assertion Markup Language (SAML) pour cette partie de confiance, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ca936-131">Under **Relying party SAML 2.0 SSO service URL**, type the Security Assertion Markup Language (SAML) service endpoint URL for this relying party trust, and then click **Next**.</span></span>  <span data-ttu-id="ca936-132">Pour **URL du service SSO SAML 2.0 de la partie de confiance**, collez la `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span><span class="sxs-lookup"><span data-stu-id="ca936-132">For the **Relying party SAML 2.0 SSO service URL**, paste the `https://login.microsoftonline.com/te/{tenant}.onmicrosoft.com/{policy}`.</span></span> <span data-ttu-id="ca936-133">Remplacez {tenant} par le nom de votre client (par exemple, contosob2c.onmicrosoft.com) et remplacez {policy} par votre nom de stratégie d’extension (par exemple, B2C_1A_TrustFrameworkExtensions).</span><span class="sxs-lookup"><span data-stu-id="ca936-133">Replace {tenant} with your tenant's name (for example, contosob2c.onmicrosoft.com), and replace the {policy} with your extensions policy name (for example, B2C_1A_TrustFrameworkExtensions).</span></span>
    > [!IMPORTANT]
    ><span data-ttu-id="ca936-134">Le nom de la stratégie est celui dont signup_or_signin hérite. Dans ce cas, il s’agit de : `B2C_1A_TrustFrameworkExtensions`.</span><span class="sxs-lookup"><span data-stu-id="ca936-134">The policy name  is the one that signup_or_signin policy inherits from, in this case it is: `B2C_1A_TrustFrameworkExtensions`.</span></span>
    ><span data-ttu-id="ca936-135">Par exemple l’URL peut être : https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span><span class="sxs-lookup"><span data-stu-id="ca936-135">For example the URL could be:   https://login.microsoftonline.com/te/**contosob2c**.onmicrosoft.com/**B2C_1A_TrustFrameworkBase**.</span></span>

    ![URL du service SSO SAML 2.0 de la partie de confiance](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-6.png)
8. <span data-ttu-id="ca936-137">Sur la page **Configurer les identificateurs**, spécifiez la même URL qu’à l’étape précédente, cliquez sur **Ajouter** pour les ajouter à la liste, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ca936-137">On the **Configure Identifiers** page, specify the same URL as the previous step, click **Add** to add them to the list, and then click **Next**.</span></span>
    <span data-ttu-id="ca936-138">![Identificateurs d’approbation de partie de confiance](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-138">![Relying party trust identifiers](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-7.png)</span></span>
9.  <span data-ttu-id="ca936-139">Dans la page **Choisir la stratégie de contrôle d’accès**, sélectionnez une stratégie puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="ca936-139">On the **Choose Access Control Policy** select a policy and click **Next**.</span></span>
    <span data-ttu-id="ca936-140">![Choisir la stratégie de contrôle d’accès](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-140">![Choose Access Control Policy](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-8.png)</span></span>
10.  <span data-ttu-id="ca936-141">Sur la page **Prêt à ajouter l’approbation**, passez en revue les paramètres, puis cliquez sur **Suivant** pour enregistrer vos informations d’approbation de partie de confiance.</span><span class="sxs-lookup"><span data-stu-id="ca936-141">On the **Ready to Add Trust** page, review the settings, and then click **Next** to save your relying party trust information.</span></span>
    <span data-ttu-id="ca936-142">![Enregistrer vos informations d’approbation de partie de confiance](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-142">![Save your relying party trust information](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-9.png)</span></span>
11.  <span data-ttu-id="ca936-143">Sur la page **Terminer**, cliquez sur **Fermer**, cette action affiche automatiquement la boîte de dialogue **Modifier les règles de revendication**.</span><span class="sxs-lookup"><span data-stu-id="ca936-143">On the **Finish** page, click **Close**, this action automatically displays the **Edit Claim Rules** dialog box.</span></span>
    <span data-ttu-id="ca936-144">![Modifier les règles de revendication](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-144">![Edit Claim Rules](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-rp-10.png)</span></span>
12. <span data-ttu-id="ca936-145">Cliquez sur **Ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="ca936-145">Click **Add Rule**.</span></span>  
      <span data-ttu-id="ca936-146">![Ajouter une nouvelle règle](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-146">![Add new rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-1.png)</span></span>
13.  <span data-ttu-id="ca936-147">Dans **Modèle de règle de revendication**, sélectionnez **Envoyer les attributs LDAP en tant que revendications**.</span><span class="sxs-lookup"><span data-stu-id="ca936-147">In **Claim rule template**, select **Send LDAP attributes as claims**.</span></span>
    <span data-ttu-id="ca936-148">![Sélectionner la règle de modèle « Envoyer les attributs LDAP comme des revendications »](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-148">![Select Send LDAP attributes as claims template rule](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-2.png)</span></span>
14.  <span data-ttu-id="ca936-149">Fournissez le **Nom de règle de revendication**.</span><span class="sxs-lookup"><span data-stu-id="ca936-149">Provide **Claim rule name**.</span></span> <span data-ttu-id="ca936-150">Pour le **Magasin d’attributs** sélectionnez **Sélectionner Active Directory**, ajoutez les revendications suivantes, puis cliquez sur **Terminer** et **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca936-150">For the **Attribute store** select **Select Active Directory** Add the following claims, then click **Finish** and **OK**.</span></span>
    <span data-ttu-id="ca936-151">![Définir les propriétés de règle](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-151">![Set rule properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-claims-3.png)</span></span>
15.  <span data-ttu-id="ca936-152">Dans le gestionnaire de serveur, sélectionnez **Approbations de partie de confiance** , puis sélectionnez l’approbation de partie de confiance vous avez créée, puis cliquez sur **Propriétés**.</span><span class="sxs-lookup"><span data-stu-id="ca936-152">In Server Manager, select **Relying Party Trusts** then select the relying party trust you created and click **Properties**.</span></span>
    <span data-ttu-id="ca936-153">![Modifier les propriétés de la partie de confiance](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-153">![Relying party edit properties](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-1.png)</span></span>
16.  <span data-ttu-id="ca936-154">Sur la fenêtre de propriétés d’approbation de partie de confiance (B2C Demo), cliquez sur l’onglet **Signature** puis cliquez sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ca936-154">One the relying party trust (B2C Demo) properties window click **Signature** tab and click **Add**.</span></span>  
    <span data-ttu-id="ca936-155">![Définir signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-155">![Set signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-2.png)</span></span>
17.  <span data-ttu-id="ca936-156">Ajoutez votre certificat de signature (fichier .cert sans clé privée).</span><span class="sxs-lookup"><span data-stu-id="ca936-156">Add your signature certificate (.cert file, without private key).</span></span>  
    ![Ajouter votre certificat de signature](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-3.png)
18.  <span data-ttu-id="ca936-158">Sur la fenêtre de propriétés d’approbation de partie de confiance (B2C Demo), cliquez sur l’onglet **Avancé** et modifiez le **Algorithme de hachage sécurisé** sur **SHA-1**, puis cliquez sur **Ok**.</span><span class="sxs-lookup"><span data-stu-id="ca936-158">On the relying party trust (B2C Demo) properties window click **Advanced** tab and change the **Secure hash algorithm** to **SHA-1**, Click **Ok**.</span></span>  
    <span data-ttu-id="ca936-159">![Définir l’algorithme de hachage sécurisé SHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-159">![Set secure hash algorithm to SHA-1](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-sig-4.png)</span></span>

## <a name="add-the-adfs-account-application-key-to-azure-ad-b2c"></a><span data-ttu-id="ca936-160">Ajouter la clé d’application de compte ADFS à Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="ca936-160">Add the ADFS account application key to Azure AD B2C</span></span>
<span data-ttu-id="ca936-161">La fédération avec les comptes ADFS requiert une clé secrète client pour le compte ADFS pour accorder la confiance à Azure AD B2C au nom de l’application.</span><span class="sxs-lookup"><span data-stu-id="ca936-161">Federation with ADFS accounts requires a client secret for ADFS account to trust Azure AD B2C on behalf of the application.</span></span> <span data-ttu-id="ca936-162">Vous devez enregistrer votre certificat ADFS dans votre client Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="ca936-162">You need to store your ADFS certificate in your Azure AD B2C tenant.</span></span> 

1.  <span data-ttu-id="ca936-163">Accédez à votre locataire Azure AD B2C, puis sélectionnez **Paramètres Azure AD B2C** > **Infrastructure d’expérience d’identité**</span><span class="sxs-lookup"><span data-stu-id="ca936-163">Go to your Azure AD B2C tenant, and select **B2C Settings** > **Identity Experience Framework**</span></span>
2.  <span data-ttu-id="ca936-164">Sélectionnez **Clés de stratégie** pour afficher les clés disponibles dans votre client.</span><span class="sxs-lookup"><span data-stu-id="ca936-164">Select **Policy Keys** to view the keys available in your tenant.</span></span>
3.  <span data-ttu-id="ca936-165">Cliquez sur **+Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="ca936-165">Click **+Add**.</span></span>
4.  <span data-ttu-id="ca936-166">Pour **Options**, utilisez **Télécharger**.</span><span class="sxs-lookup"><span data-stu-id="ca936-166">For **Options**, use **Upload**.</span></span>
5.  <span data-ttu-id="ca936-167">Pour **Nom**, utilisez `ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="ca936-167">For **Name**, use `ADFSSamlCert`.</span></span>  
    <span data-ttu-id="ca936-168">Il est possible que le préfixe `B2C_1A_` soit ajouté automatiquement.</span><span class="sxs-lookup"><span data-stu-id="ca936-168">The prefix `B2C_1A_` might be added automatically.</span></span>
6.  <span data-ttu-id="ca936-169">Dans le Télécharger fichier,** sélectionnez votre fichier de certificat .pfx avec la clé privée.</span><span class="sxs-lookup"><span data-stu-id="ca936-169">In the File upload,** select your certificate .pfx file with private key.</span></span> <span data-ttu-id="ca936-170">Remarque : ce certificat (avec la clé privée) doit être le même que celui qui délivré et utilisé pour la partie de confiance d’ADFS.</span><span class="sxs-lookup"><span data-stu-id="ca936-170">Note: this certificate (with the private key) should be the same one that issued and used for the ADFS relying party.</span></span>
<span data-ttu-id="ca936-171">![Télécharger la clé de stratégie](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span><span class="sxs-lookup"><span data-stu-id="ca936-171">![Upload policy key](media/active-directory-b2c-custom-setup-adfs2016-idp/aadb2c-ief-setup-adfs2016-idp-cert.png)</span></span>
7.  <span data-ttu-id="ca936-172">Cliquez sur **Créer**</span><span class="sxs-lookup"><span data-stu-id="ca936-172">Click **Create**</span></span>
8.  <span data-ttu-id="ca936-173">Vérifiez que vous avez créé la clé `B2C_1A_ADFSSamlCert`.</span><span class="sxs-lookup"><span data-stu-id="ca936-173">Confirm that you've created the key `B2C_1A_ADFSSamlCert`.</span></span>

## <a name="add-a-claims-provider-in-your-extension-policy"></a><span data-ttu-id="ca936-174">Ajouter un fournisseur de revendications à une stratégie d’extension</span><span class="sxs-lookup"><span data-stu-id="ca936-174">Add a claims provider in your extension policy</span></span>
<span data-ttu-id="ca936-175">Si vous souhaitez que les utilisateurs se connectent à l’aide d’un compte ADFS, vous devez définir le compte ADFS comme fournisseur de revendications.</span><span class="sxs-lookup"><span data-stu-id="ca936-175">If you want users to sign in by using ADFS account, you need to define ADFS account as a claims provider.</span></span> <span data-ttu-id="ca936-176">En d’autres termes, vous devez spécifier un point de terminaison avec lequel Azure AD B2C communiquera.</span><span class="sxs-lookup"><span data-stu-id="ca936-176">In other words, you need to specify an endpoint that Azure AD B2C communicates with.</span></span> <span data-ttu-id="ca936-177">Le point de terminaison fournit un ensemble de revendications utilisées par Azure AD B2C pour vérifier qu’un utilisateur spécifique s’est authentifié.</span><span class="sxs-lookup"><span data-stu-id="ca936-177">The endpoint provides a set of claims that are used by Azure AD B2C to verify that a specific user has authenticated.</span></span>

<span data-ttu-id="ca936-178">Définissez ADFS comme fournisseur de revendications, en ajoutant le nœud `<ClaimsProvider>` dans votre fichier de stratégie d’extension :</span><span class="sxs-lookup"><span data-stu-id="ca936-178">Define ADFS as a claims provider, by adding `<ClaimsProvider>` node in your extension policy file:</span></span>

1. <span data-ttu-id="ca936-179">Ouvrez le fichier de stratégie d’extension (TrustFrameworkExtensions.xml) à partir de votre répertoire de travail.</span><span class="sxs-lookup"><span data-stu-id="ca936-179">Open the extension policy file (TrustFrameworkExtensions.xml) from your working directory.</span></span> <span data-ttu-id="ca936-180">Si vous avez besoin d’un éditeur XML, [essayez Visual Studio Code](https://code.visualstudio.com/download), un éditeur multiplateforme léger.</span><span class="sxs-lookup"><span data-stu-id="ca936-180">If you need an XML editor, [try Visual Studio Code](https://code.visualstudio.com/download), a lightweight cross-platform editor.</span></span>
2. <span data-ttu-id="ca936-181">Recherchez la section `<ClaimsProviders>`</span><span class="sxs-lookup"><span data-stu-id="ca936-181">Find the `<ClaimsProviders>` section</span></span>
3. <span data-ttu-id="ca936-182">Ajoutez l’extrait XML suivant sous l’élément `ClaimsProviders` et remplacez `identityProvider` par votre serveur DNS (valeur arbitraire qui indique votre domaine), puis enregistrez le fichier.</span><span class="sxs-lookup"><span data-stu-id="ca936-182">Add the following XML snippet under the `ClaimsProviders` element and replace `identityProvider` with your DNS (Arbitrary value that indicates your domain), and save the file.</span></span> 

```xml
<ClaimsProvider>
    <Domain>contoso.com</Domain>
    <DisplayName>Contoso ADFS</DisplayName>
    <TechnicalProfiles>
    <TechnicalProfile Id="Contoso-SAML2">
        <DisplayName>Contoso ADFS</DisplayName>
        <Description>Login with your Contoso account</Description>
        <Protocol Name="SAML2"/>
        <Metadata>
        <Item Key="RequestsSigned">false</Item>
        <Item Key="WantsEncryptedAssertions">false</Item>
        <Item Key="PartnerEntity">https://{your_ADFS_domain}/federationmetadata/2007-06/federationmetadata.xml</Item>
        </Metadata>
        <CryptographicKeys>
        <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_ADFSSamlCert"/>
        </CryptographicKeys>
        <OutputClaims>
        <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userPrincipalName" />
        <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
        <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
        <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
        <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="name"/>
        <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="contoso.com" />
        <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
        </OutputClaims>
        <OutputClaimsTransformations>
        <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
        <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
        <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
        <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
        </OutputClaimsTransformations>
        <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
    </TechnicalProfile>
    </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="register-the-adfs-account-claims-provider-to-sign-up-or-sign-in-user-journey"></a><span data-ttu-id="ca936-183">Inscription du fournisseur de revendications de compte ADFS à un parcours utilisateur Inscription ou Connexion</span><span class="sxs-lookup"><span data-stu-id="ca936-183">Register the ADFS account claims provider to Sign up or Sign in user journey</span></span>
<span data-ttu-id="ca936-184">À ce stade, le fournisseur d’identité a été configuré.</span><span class="sxs-lookup"><span data-stu-id="ca936-184">At this point, the identity provider has been set up.</span></span>  <span data-ttu-id="ca936-185">Toutefois, il n’est disponible dans aucun des écrans d’inscription/de connexion.</span><span class="sxs-lookup"><span data-stu-id="ca936-185">However, it is not available in any of the sign-up/sign-in screens.</span></span> <span data-ttu-id="ca936-186">Maintenant vous devez ajouter le fournisseur d’identité du compte AD FS au parcours `SignUpOrSignIn` de votre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ca936-186">Now you need to add the ADFS account identity provider to your user `SignUpOrSignIn` user journey.</span></span> <span data-ttu-id="ca936-187">Pour le rendre disponible, nous créons un doublon d’un modèle de parcours utilisateur existant.</span><span class="sxs-lookup"><span data-stu-id="ca936-187">To make it available, we create a duplicate of an existing template user journey.</span></span>  <span data-ttu-id="ca936-188">Ensuite, nous le modifions pour qu’il comporte le fournisseur d’identité ADFS :</span><span class="sxs-lookup"><span data-stu-id="ca936-188">Then, we modify it so it includes the ADFS identity provider:</span></span>
    >[!NOTE]
    >If you previously copied the `<UserJourneys>` element from base file of your policy to the extension file (TrustFrameworkExtensions.xml) you can skip this section.
1.  <span data-ttu-id="ca936-189">Ouvrez le fichier de base de votre stratégie (par exemple, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="ca936-189">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2.  <span data-ttu-id="ca936-190">Recherchez l’élément `<UserJourneys>` et copiez la totalité du contenu du nœud `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="ca936-190">Find the `<UserJourneys>` element and copy the entire content of `<UserJourneys>` node.</span></span>
3.  <span data-ttu-id="ca936-191">Ouvrez le fichier d’extension (par exemple, TrustFrameworkExtensions.xml), puis recherchez l’élément `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="ca936-191">Open the extension file (for example, TrustFrameworkExtensions.xml) and find the `<UserJourneys>` element.</span></span> <span data-ttu-id="ca936-192">Si l’élément n’existe pas, ajoutez-en un.</span><span class="sxs-lookup"><span data-stu-id="ca936-192">If the element doesn't exist, add one.</span></span>
4.  <span data-ttu-id="ca936-193">Collez l’intégralité du contenu du nœud `<UserJournesy>` que vous avez copié en tant qu’enfant de l’élément `<UserJourneys>`.</span><span class="sxs-lookup"><span data-stu-id="ca936-193">Paste the entire content of `<UserJournesy>` node that you copied as a child of the `<UserJourneys>` element.</span></span>

### <a name="display-the-button"></a><span data-ttu-id="ca936-194">Afficher le bouton</span><span class="sxs-lookup"><span data-stu-id="ca936-194">Display the button</span></span>
<span data-ttu-id="ca936-195">L’élément `<ClaimsProviderSelections>` définit la liste des options de sélection du fournisseur de revendications et leur ordre.</span><span class="sxs-lookup"><span data-stu-id="ca936-195">The `<ClaimsProviderSelections>` element defines the list of claims provider selection options and their order.</span></span>  <span data-ttu-id="ca936-196">L’élément `<ClaimsProviderSelection>` est analogue à un bouton de fournisseur d’identité sur une page d’inscription/de connexion.</span><span class="sxs-lookup"><span data-stu-id="ca936-196">`<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up/sign-in page.</span></span> <span data-ttu-id="ca936-197">Si vous ajoutez un élément `<ClaimsProviderSelection>` au compte ADFS, un nouveau bouton apparaît quand un utilisateur accède à la page.</span><span class="sxs-lookup"><span data-stu-id="ca936-197">If you add a `<ClaimsProviderSelection>` element for  ADFS account, a new button shows up when a user lands on the page.</span></span> <span data-ttu-id="ca936-198">Pour ajouter cet élément :</span><span class="sxs-lookup"><span data-stu-id="ca936-198">To add this element:</span></span>

1.  <span data-ttu-id="ca936-199">Recherchez le nœud `<UserJourney>` incluant `Id="SignUpOrSignIn"` dans le parcours utilisateur que vous avez copié.</span><span class="sxs-lookup"><span data-stu-id="ca936-199">Find the `<UserJourney>` node that includes `Id="SignUpOrSignIn"` in the user journey that you copied.</span></span>
2.  <span data-ttu-id="ca936-200">Localisez le nœud `<OrchestrationStep>` qui inclut `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="ca936-200">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
3.  <span data-ttu-id="ca936-201">Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsProviderSelections>` :</span><span class="sxs-lookup"><span data-stu-id="ca936-201">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```
### <a name="link-the-button-to-an-action"></a><span data-ttu-id="ca936-202">Lier le bouton à une action</span><span class="sxs-lookup"><span data-stu-id="ca936-202">Link the button to an action</span></span>

<span data-ttu-id="ca936-203">Maintenant que vous avez un bouton en place, vous devez le lier à une action.</span><span class="sxs-lookup"><span data-stu-id="ca936-203">Now that you have a button in place, you need to link it to an action.</span></span> <span data-ttu-id="ca936-204">L’action est, dans ce cas, la communication d’Azure AD B2C avec le compte ADFS pour recevoir un jeton.</span><span class="sxs-lookup"><span data-stu-id="ca936-204">The action, in this case, is for Azure AD B2C to communicate with ADFS account to receive a token.</span></span> <span data-ttu-id="ca936-205">Liez le bouton à une action en liant le profil technique de votre fournisseur de revendications compte ADFS :</span><span class="sxs-lookup"><span data-stu-id="ca936-205">Link the button to an action by linking the technical profile for your ADFS account claims provider:</span></span>

1.  <span data-ttu-id="ca936-206">Recherchez l’élément `<OrchestrationStep>` qui inclut `Order="2"` dans le nœud `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="ca936-206">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="ca936-207">Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsExchanges>` :</span><span class="sxs-lookup"><span data-stu-id="ca936-207">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

> [!NOTE]
> * <span data-ttu-id="ca936-208">Assurez-vous que `Id` a la même valeur que celle de `TargetClaimsExchangeId` dans la section précédente.</span><span class="sxs-lookup"><span data-stu-id="ca936-208">Ensure the `Id` has the same value as that of `TargetClaimsExchangeId` in the preceding section.</span></span>
> * <span data-ttu-id="ca936-209">Vérifiez que `TechnicalProfileReferenceId` est défini sur le profil de technique que vous avez créé plus haut (Contoso-SAML2).</span><span class="sxs-lookup"><span data-stu-id="ca936-209">Ensure `TechnicalProfileReferenceId` is set to the technical profile you created earlier (Contoso-SAML2).</span></span>

## <a name="upload-the-policy-to-your-tenant"></a><span data-ttu-id="ca936-210">Charger la stratégie sur votre client</span><span class="sxs-lookup"><span data-stu-id="ca936-210">Upload the policy to your tenant</span></span>
1.  <span data-ttu-id="ca936-211">Dans le [portail Azure](https://portal.azure.com), passez au [contexte de votre locataire Azure AD B2C](active-directory-b2c-navigate-to-b2c-context.md) et ouvrez le panneau **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="ca936-211">In the [Azure portal](https://portal.azure.com), switch into the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and open the **Azure AD B2C** blade.</span></span>
2.  <span data-ttu-id="ca936-212">Sélectionnez **Infrastructure d’expérience d’identité**.</span><span class="sxs-lookup"><span data-stu-id="ca936-212">Select **Identity Experience Framework**.</span></span>
3.  <span data-ttu-id="ca936-213">Ouvrez le panneau **Toutes les stratégies**.</span><span class="sxs-lookup"><span data-stu-id="ca936-213">Open the **All Policies** blade.</span></span>
4.  <span data-ttu-id="ca936-214">Sélectionnez **Charger la stratégie**.</span><span class="sxs-lookup"><span data-stu-id="ca936-214">Select **Upload Policy**.</span></span>
5.  <span data-ttu-id="ca936-215">Cochez la case **Remplacer la stratégie si elle existe**.</span><span class="sxs-lookup"><span data-stu-id="ca936-215">Check **Overwrite the policy if it exists** box.</span></span>
6.  <span data-ttu-id="ca936-216">**Téléchargez** TrustFrameworkExtensions.xml et vérifiez que sa validation n’échoue pas</span><span class="sxs-lookup"><span data-stu-id="ca936-216">**Upload** TrustFrameworkExtensions.xml and ensure that it does not fail the validation</span></span>

## <a name="test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="ca936-217">Tester la stratégie personnalisée en utilisant Exécuter maintenant</span><span class="sxs-lookup"><span data-stu-id="ca936-217">Test the custom policy by using Run Now</span></span>
1.  <span data-ttu-id="ca936-218">Ouvrez **Paramètres Azure AD B2C** et accédez à **Infrastructure d’expérience d’identité**.</span><span class="sxs-lookup"><span data-stu-id="ca936-218">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="ca936-219">Ouvrez **B2C_1A_signup_signin**, la stratégie personnalisée de partie de confiance que vous avez chargée.</span><span class="sxs-lookup"><span data-stu-id="ca936-219">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="ca936-220">Sélectionnez **Exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="ca936-220">Select **Run now**.</span></span>
3.  <span data-ttu-id="ca936-221">Vous devriez être en mesure de vous connecter à l’aide de votre compte ADFS.</span><span class="sxs-lookup"><span data-stu-id="ca936-221">You should be able to sign in using ADFS account.</span></span>

## <a name="optional-register-the-adfs-account-claims-provider-to-profile-edit-user-journey"></a><span data-ttu-id="ca936-222">[Facultatif] Inscription du fournisseur de revendications de compte ADFS à un parcours utilisateur Modification de profil</span><span class="sxs-lookup"><span data-stu-id="ca936-222">[Optional] Register the ADFS account claims provider to Profile-Edit user journey</span></span>
<span data-ttu-id="ca936-223">Vous pouvez également ajouter le fournisseur d’identité du compte ADFS au parcours utilisateur `ProfileEdit` de votre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="ca936-223">You may want to add the ADFS account identity provider also to your user `ProfileEdit` user journey.</span></span> <span data-ttu-id="ca936-224">Pour le rendre disponible, nous répétons les deux dernières étapes :</span><span class="sxs-lookup"><span data-stu-id="ca936-224">To make it available, we repeat the last two steps:</span></span>

### <a name="display-the-button"></a><span data-ttu-id="ca936-225">Afficher le bouton</span><span class="sxs-lookup"><span data-stu-id="ca936-225">Display the button</span></span>
1.  <span data-ttu-id="ca936-226">Ouvrez le fichier d’extension de votre stratégie (par exemple, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="ca936-226">Open the extension file of your policy (for example, TrustFrameworkExtensions.xml).</span></span>
2.  <span data-ttu-id="ca936-227">Recherchez le nœud `<UserJourney>` incluant `Id="ProfileEdit"` dans le parcours utilisateur que vous avez copié.</span><span class="sxs-lookup"><span data-stu-id="ca936-227">Find the `<UserJourney>` node that includes `Id="ProfileEdit"` in the user journey that you copied.</span></span>
3.  <span data-ttu-id="ca936-228">Localisez le nœud `<OrchestrationStep>` qui inclut `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="ca936-228">Locate the `<OrchestrationStep>` node that includes `Order="1"`</span></span>
4.  <span data-ttu-id="ca936-229">Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsProviderSelections>` :</span><span class="sxs-lookup"><span data-stu-id="ca936-229">Add following XML snippet under `<ClaimsProviderSelections>` node:</span></span>

```xml
<ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
```

### <a name="link-the-button-to-an-action"></a><span data-ttu-id="ca936-230">Lier le bouton à une action</span><span class="sxs-lookup"><span data-stu-id="ca936-230">Link the button to an action</span></span>
1.  <span data-ttu-id="ca936-231">Recherchez l’élément `<OrchestrationStep>` qui inclut `Order="2"` dans le nœud `<UserJourney>`.</span><span class="sxs-lookup"><span data-stu-id="ca936-231">Find the `<OrchestrationStep>` that includes `Order="2"` in the `<UserJourney>` node.</span></span>
2.  <span data-ttu-id="ca936-232">Ajoutez l’extrait de code XML suivant sous le nœud `<ClaimsExchanges>` :</span><span class="sxs-lookup"><span data-stu-id="ca936-232">Add following XML snippet under `<ClaimsExchanges>` node:</span></span>

```xml
<ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="Contoso-SAML2" />
```

### <a name="test-the-custom-profile-edit-policy-by-using-run-now"></a><span data-ttu-id="ca936-233">Tester la stratégie personnalisée de modification de profil en utilisant Exécuter maintenant</span><span class="sxs-lookup"><span data-stu-id="ca936-233">Test the custom Profile-Edit policy by using Run Now</span></span>
1.  <span data-ttu-id="ca936-234">Ouvrez **Paramètres Azure AD B2C** et accédez à **Infrastructure d’expérience d’identité**.</span><span class="sxs-lookup"><span data-stu-id="ca936-234">Open **Azure AD B2C Settings** and go to **Identity Experience Framework**.</span></span>
2.  <span data-ttu-id="ca936-235">Ouvrez **B2C_1A_ProfileEdit**, la stratégie personnalisée de partie de confiance que vous avez chargée.</span><span class="sxs-lookup"><span data-stu-id="ca936-235">Open **B2C_1A_ProfileEdit**, the relying party (RP) custom policy that you uploaded.</span></span> <span data-ttu-id="ca936-236">Sélectionnez **Exécuter maintenant**.</span><span class="sxs-lookup"><span data-stu-id="ca936-236">Select **Run now**.</span></span>
3.  <span data-ttu-id="ca936-237">Vous devriez être en mesure de vous connecter à l’aide de votre compte ADFS.</span><span class="sxs-lookup"><span data-stu-id="ca936-237">You should be able to sign in using ADFS account.</span></span>

## <a name="download-the-complete-policy-files"></a><span data-ttu-id="ca936-238">Télécharger les fichiers de stratégie complets</span><span class="sxs-lookup"><span data-stu-id="ca936-238">Download the complete policy files</span></span>
<span data-ttu-id="ca936-239">Facultatif : nous vous recommandons de créer votre scénario à l’aide de vos propres fichiers de stratégie personnalisée après avoir effectué la prise en main des stratégies personnalisées.</span><span class="sxs-lookup"><span data-stu-id="ca936-239">Optional: We recommend you build your scenario using your own Custom policy files after completing the Getting Started with Custom Policies walk through.</span></span> [<span data-ttu-id="ca936-240">Exemples de fichiers de stratégie pour référence uniquement</span><span class="sxs-lookup"><span data-stu-id="ca936-240">Policy sample files for reference only</span></span>](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-setup-adfs2016-app)
