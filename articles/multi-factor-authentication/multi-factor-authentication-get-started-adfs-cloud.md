---
title: "Sécurisation des ressources de cloud avec Azure MFA et AD FS | Microsoft Docs"
description: "Voici la page d'authentification multifacteur Azure qui explique la prise en main de l'authentification multifacteur Azure et d’AD FS 2.0 dans le cloud."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 6cf4ec4f777ea1f2b852945ab82da2547946f378
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="e9b0c-103">Sécurisation des ressources de cloud avec le serveur Azure Multi-Factor Authentication et AD FS</span><span class="sxs-lookup"><span data-stu-id="e9b0c-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="e9b0c-104">Si votre organisation est fédérée avec Azure Active Directory AD, utilisez l’authentification multifacteur Azure ou les services de fédération d’Active Directory (AD FS) pour sécuriser les ressources auxquelles Azure AD accède.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) to secure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="e9b0c-105">Utilisez les procédures suivantes pour sécuriser les ressources Azure Active Directory avec l’authentification multifacteur Azure ou les services de fédération d’Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-105">Use the following procedures to secure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="e9b0c-106">Sécurisation des ressources Azure AD à l’aide d’AD FS</span><span class="sxs-lookup"><span data-stu-id="e9b0c-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="e9b0c-107">Pour sécuriser vos ressources de cloud, configurez une règle de revendication afin que les services de fédération Active Directory émettent la revendication multipleauthn lorsqu’un utilisateur effectue la vérification en deux étapes avec succès.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-107">To secure your cloud resource, set up a claims rule so that Active Directory Federation Services emits the multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="e9b0c-108">Cette revendication est transmise à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-108">This claim is passed on to Azure AD.</span></span> <span data-ttu-id="e9b0c-109">Suivez cette procédure pour les différentes étapes :</span><span class="sxs-lookup"><span data-stu-id="e9b0c-109">Follow this procedure to walk through the steps:</span></span>


1. <span data-ttu-id="e9b0c-110">Ouvrez Gestion AD FS.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="e9b0c-111">Sur la gauche, sélectionnez **Approbations de partie de confiance**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-111">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="e9b0c-112">Cliquez avec le bouton droit sur **Plateforme d’identité Microsoft Office 365** et sélectionnez **Modifier les règles de revendication**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="e9b0c-114">Sous Règles de transformation d’émission, cliquez sur **Ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="e9b0c-116">Dans l’Assistant Ajout de règle de revendication de transformation, sélectionnez **Passer ou filtrer une revendication entrante** dans la liste déroulante et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-116">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="e9b0c-118">Nommez votre règle.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="e9b0c-119">Sélectionnez **Références des méthodes d’authentification** pour le type de revendication entrante.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-119">Select **Authentication Methods References** as the Incoming claim type.</span></span>
8. <span data-ttu-id="e9b0c-120">Sélectionnez **Transférer toutes les valeurs de revendication**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="e9b0c-121">![Assistant Ajouter une règle de revendication de transformation](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="e9b0c-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="e9b0c-122">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-122">Click **Finish**.</span></span> <span data-ttu-id="e9b0c-123">Fermez la console de gestion AD FS.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-123">Close the AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="e9b0c-124">Adresses IP de confiance pour les utilisateurs fédérés</span><span class="sxs-lookup"><span data-stu-id="e9b0c-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="e9b0c-125">Les adresses IP approuvées permettent aux administrateurs de contourner la vérification en deux étapes pour des adresses IP spécifiques ou pour les utilisateurs fédérés qui ont des requêtes provenant de leur propre intranet.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-125">Trusted IPs allow administrators to by-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="e9b0c-126">Les sections suivantes décrivent comment configurer des adresses IP approuvées Azure Multi-Factor Authentication avec des utilisateurs fédérés et comment contourner la vérification en deux étapes, lorsqu’une requête provient d’un intranet d’utilisateurs fédérés.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-126">The following sections describe how to configure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="e9b0c-127">Pour cela, vous devez configurer AD FS pour utiliser un passthrough ou filtrer un modèle de revendication entrante avec le type de revendication Dans le périmètre du réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-127">This is achieved by configuring AD FS to use a pass-through or filter an incoming claim template with the Inside Corporate Network claim type.</span></span>

<span data-ttu-id="e9b0c-128">Cet exemple utilise Office 365 pour nos approbations de la partie de confiance.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-the-ad-fs-claims-rules"></a><span data-ttu-id="e9b0c-129">Configuration des règles de revendications AD FS</span><span class="sxs-lookup"><span data-stu-id="e9b0c-129">Configure the AD FS claims rules</span></span>
<span data-ttu-id="e9b0c-130">La première chose à faire consiste à configurer les revendications AD FS.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-130">The first thing we need to do is to configure the AD FS claims.</span></span> <span data-ttu-id="e9b0c-131">Créez deux règles de revendications : une pour le type de revendication Dans le périmètre du réseau d’entreprise et l’autre pour maintenir les utilisateurs connectés.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-131">Create two claims rules, one for the Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="e9b0c-132">Ouvrez Gestion AD FS.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="e9b0c-133">Sur la gauche, sélectionnez **Approbations de partie de confiance**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-133">On the left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="e9b0c-134">Cliquez avec le bouton droit sur la **Plateforme d’identité Microsoft Office 365** et sélectionnez **Modifier les règles de revendication…**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="e9b0c-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="e9b0c-135">Sous Règles de transformation d’émission, cliquez sur **Ajouter une règle.**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="e9b0c-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="e9b0c-136">Dans l’Assistant Ajout de règle de revendication de transformation, sélectionnez **Passer ou filtrer une revendication entrante** dans la liste déroulante et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-136">On the Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from the drop-down and click **Next**.</span></span>
   <span data-ttu-id="e9b0c-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="e9b0c-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="e9b0c-138">Dans la zone en regard du nom de la règle de revendication, nommez votre règle.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-138">In the box next to Claim rule name, give your rule a name.</span></span> <span data-ttu-id="e9b0c-139">Par exemple : InsideCorpNet.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="e9b0c-140">Dans la liste déroulante, en regard du type de revendication entrante, sélectionnez **Dans le périmètre du réseau d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-140">From the drop-down, next to Incoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="e9b0c-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="e9b0c-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="e9b0c-142">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-142">Click **Finish**.</span></span>
9. <span data-ttu-id="e9b0c-143">Sous Règles de transformation d’émission, cliquez sur **Ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="e9b0c-144">Dans l’Assistant Ajout de règle de revendication de transformation, sélectionnez **Envoyer les revendications en utilisant une règle personnalisée** dans la liste déroulante et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-144">On the Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from the drop-down and click **Next**.</span></span>
11. <span data-ttu-id="e9b0c-145">Dans la zone sous Nom de la règle de revendication : entrez *Keep Users Signed In (Maintenir les utilisateurs connectés)*.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-145">In the box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="e9b0c-146">Dans la zone Règle personnalisée, entrez :</span><span class="sxs-lookup"><span data-stu-id="e9b0c-146">In the Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="e9b0c-148">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-148">Click **Finish**.</span></span>
14. <span data-ttu-id="e9b0c-149">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-149">Click **Apply**.</span></span>
15. <span data-ttu-id="e9b0c-150">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-150">Click **Ok**.</span></span>
16. <span data-ttu-id="e9b0c-151">Fermez Gestion AD FS.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="e9b0c-152">Configuration d'adresses IP de confiance Azure Multi-Factor Authentication avec des utilisateurs fédérés</span><span class="sxs-lookup"><span data-stu-id="e9b0c-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="e9b0c-153">Maintenant que les revendications sont en place, nous pouvons configurer des adresses IP approuvées.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-153">Now that the claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="e9b0c-154">Connectez-vous au [portail Azure Classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="e9b0c-154">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="e9b0c-155">Cliquez à gauche sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-155">On the left, click **Active Directory**.</span></span>
3. <span data-ttu-id="e9b0c-156">Sous Annuaire, sélectionnez l’annuaire dans lequel vous souhaitez configurer les adresses IP approuvées.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-156">Under Directory, select the directory where you want to set up trusted IPs.</span></span>
4. <span data-ttu-id="e9b0c-157">Dans l’annuaire que vous avez sélectionné, cliquez sur **Configurer**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-157">On the Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="e9b0c-158">Dans la section Authentification multifacteur, cliquez sur **Gérer les paramètres du service**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-158">In the multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="e9b0c-159">Sur la page Paramètres du service, sous Adresses IP approuvées, sélectionnez **Ignorer l’authentification multifacteur pour les demandes issues d’utilisateurs fédérés provenant de mon intranet**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-159">On the Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="e9b0c-161">Cliquez sur **save**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-161">Click **save**.</span></span>
8. <span data-ttu-id="e9b0c-162">Une fois les mises à jour appliquées, cliquez sur **Fermer**.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-162">Once the updates have been applied, click **close**.</span></span>

<span data-ttu-id="e9b0c-163">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="e9b0c-163">That’s it!</span></span> <span data-ttu-id="e9b0c-164">À ce stade, les utilisateurs fédérés d'Office 365 doivent pouvoir utiliser uniquement MFA lorsqu'une revendication provient de l'extérieur de l'intranet de l'entreprise.</span><span class="sxs-lookup"><span data-stu-id="e9b0c-164">At this point, federated Office 365 users should only have to use MFA when a claim originates from outside the corporate intranet.</span></span>
