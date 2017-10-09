---
title: aaaSecure des ressources de cloud avec Azure MFA et AD FS | Documents Microsoft
description: "Il s’agit de page d’authentification multifacteur Azure hello qui décrit comment tooget main d’Azure MFA et AD FS dans le cloud de hello."
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
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a><span data-ttu-id="79154-103">Sécurisation des ressources de cloud avec le serveur Azure Multi-Factor Authentication et AD FS</span><span class="sxs-lookup"><span data-stu-id="79154-103">Securing cloud resources with Azure Multi-Factor Authentication and AD FS</span></span>
<span data-ttu-id="79154-104">Si votre organisation est fédérée avec Azure Active Directory, utilisez l’authentification multifacteur Azure ou des ressources de toosecure de Services de fédération Active Directory (AD FS) qui sont accessibles par Azure AD.</span><span class="sxs-lookup"><span data-stu-id="79154-104">If your organization is federated with Azure Active Directory, use Azure Multi-Factor Authentication or Active Directory Federation Services (AD FS) toosecure resources that are accessed by Azure AD.</span></span> <span data-ttu-id="79154-105">Utilisez hello suivant les procédures toosecure Azure les ressources Active Directory avec Azure multi-Factor Authentication ou Active Directory Federation Services.</span><span class="sxs-lookup"><span data-stu-id="79154-105">Use hello following procedures toosecure Azure Active Directory resources with either Azure Multi-Factor Authentication or Active Directory Federation Services.</span></span>

## <a name="secure-azure-ad-resources-using-ad-fs"></a><span data-ttu-id="79154-106">Sécurisation des ressources Azure AD à l’aide d’AD FS</span><span class="sxs-lookup"><span data-stu-id="79154-106">Secure Azure AD resources using AD FS</span></span>
<span data-ttu-id="79154-107">toosecure vos ressources de cloud, configurez une règle de revendication afin que les Services de fédération Active Directory émet hello multipleauthn revendication lorsqu’un utilisateur effectue une vérification en deux étapes avec succès.</span><span class="sxs-lookup"><span data-stu-id="79154-107">toosecure your cloud resource, set up a claims rule so that Active Directory Federation Services emits hello multipleauthn claim when a user performs two-step verification successfully.</span></span> <span data-ttu-id="79154-108">Cette revendication est passée sur tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="79154-108">This claim is passed on tooAzure AD.</span></span> <span data-ttu-id="79154-109">Suivez cette toowalk procédure étapes hello :</span><span class="sxs-lookup"><span data-stu-id="79154-109">Follow this procedure toowalk through hello steps:</span></span>


1. <span data-ttu-id="79154-110">Ouvrez Gestion AD FS.</span><span class="sxs-lookup"><span data-stu-id="79154-110">Open AD FS Management.</span></span>
2. <span data-ttu-id="79154-111">Sur hello gauche, sélectionnez **confiance**.</span><span class="sxs-lookup"><span data-stu-id="79154-111">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="79154-112">Cliquez avec le bouton droit sur **Plateforme d’identité Microsoft Office 365** et sélectionnez **Modifier les règles de revendication**.</span><span class="sxs-lookup"><span data-stu-id="79154-112">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. <span data-ttu-id="79154-114">Sous Règles de transformation d’émission, cliquez sur **Ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="79154-114">On Issuance Transform Rules, click **Add Rule**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. <span data-ttu-id="79154-116">On hello ajouter un Assistant de règle de revendication transformer, sélectionnez **passer ou filtrer une revendication entrante** dans hello de liste déroulante, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="79154-116">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. <span data-ttu-id="79154-118">Nommez votre règle.</span><span class="sxs-lookup"><span data-stu-id="79154-118">Give your rule a name.</span></span> 
7. <span data-ttu-id="79154-119">Sélectionnez **références des méthodes d’authentification** comme hello entrants le type de revendication.</span><span class="sxs-lookup"><span data-stu-id="79154-119">Select **Authentication Methods References** as hello Incoming claim type.</span></span>
8. <span data-ttu-id="79154-120">Sélectionnez **Transférer toutes les valeurs de revendication**.</span><span class="sxs-lookup"><span data-stu-id="79154-120">Select **Pass through all claim values**.</span></span>
    <span data-ttu-id="79154-121">![Assistant Ajouter une règle de revendication de transformation](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span><span class="sxs-lookup"><span data-stu-id="79154-121">![Add Transform Claim Rule Wizard](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)</span></span>
9. <span data-ttu-id="79154-122">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="79154-122">Click **Finish**.</span></span> <span data-ttu-id="79154-123">Fermez la console de gestion ADFS hello AD.</span><span class="sxs-lookup"><span data-stu-id="79154-123">Close hello AD FS Management console.</span></span>

## <a name="trusted-ips-for-federated-users"></a><span data-ttu-id="79154-124">Adresses IP de confiance pour les utilisateurs fédérés</span><span class="sxs-lookup"><span data-stu-id="79154-124">Trusted IPs for federated users</span></span>
<span data-ttu-id="79154-125">Adresses IP approuvées permettent aux administrateurs de vérification d’en deux étapes tooby-test pour des adresses IP spécifiques, ou pour les utilisateurs fédérés qui possèdent leur propre intranet d’origine à partir de requêtes.</span><span class="sxs-lookup"><span data-stu-id="79154-125">Trusted IPs allow administrators tooby-pass two-step verification for specific IP addresses, or for federated users that have requests originating from within their own intranet.</span></span> <span data-ttu-id="79154-126">Hello sections suivantes décrivent comment tooconfigure approuvées Azure multi-Factor Authentication avec les utilisateurs fédérés et contourner en deux étapes si la vérification une demande provient d’un intranet d’utilisateurs fédérés des adresses IP.</span><span class="sxs-lookup"><span data-stu-id="79154-126">hello following sections describe how tooconfigure Azure Multi-Factor Authentication Trusted IPs with federated users and by-pass two-step verification when a request originates from within a federated users intranet.</span></span> <span data-ttu-id="79154-127">Cela est possible en configurant les services AD FS toouse direct ou filtrer un modèle de revendication entrante avec hello type de revendication à l’intérieur d’un réseau d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="79154-127">This is achieved by configuring AD FS toouse a pass-through or filter an incoming claim template with hello Inside Corporate Network claim type.</span></span>

<span data-ttu-id="79154-128">Cet exemple utilise Office 365 pour nos approbations de la partie de confiance.</span><span class="sxs-lookup"><span data-stu-id="79154-128">This example uses Office 365 for our Relying Party Trusts.</span></span>

### <a name="configure-hello-ad-fs-claims-rules"></a><span data-ttu-id="79154-129">Configurer les règles de revendications hello AD FS</span><span class="sxs-lookup"><span data-stu-id="79154-129">Configure hello AD FS claims rules</span></span>
<span data-ttu-id="79154-130">Hello première chose toodo est tooconfigure hello AD FS revendications.</span><span class="sxs-lookup"><span data-stu-id="79154-130">hello first thing we need toodo is tooconfigure hello AD FS claims.</span></span> <span data-ttu-id="79154-131">Créez deux règles de revendications, l’autre pour hello à l’intérieur d’un réseau d’entreprise de revendication type et l’autre pour maintenir la connexion des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="79154-131">Create two claims rules, one for hello Inside Corporate Network claim type and an additional one for keeping our users signed in.</span></span>

1. <span data-ttu-id="79154-132">Ouvrez Gestion AD FS.</span><span class="sxs-lookup"><span data-stu-id="79154-132">Open AD FS Management.</span></span>
2. <span data-ttu-id="79154-133">Sur hello gauche, sélectionnez **confiance**.</span><span class="sxs-lookup"><span data-stu-id="79154-133">On hello left, select **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="79154-134">Cliquez avec le bouton droit sur la **Plateforme d’identité Microsoft Office 365** et sélectionnez **Modifier les règles de revendication…**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span><span class="sxs-lookup"><span data-stu-id="79154-134">Right-click on **Microsoft Office 365 Identity Platform** and select **Edit Claim Rules…**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)</span></span>
4. <span data-ttu-id="79154-135">Sous Règles de transformation d’émission, cliquez sur **Ajouter une règle.**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span><span class="sxs-lookup"><span data-stu-id="79154-135">On Issuance Transform Rules, click **Add Rule.**
![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)</span></span>
5. <span data-ttu-id="79154-136">On hello ajouter un Assistant de règle de revendication transformer, sélectionnez **passer ou filtrer une revendication entrante** dans hello de liste déroulante, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="79154-136">On hello Add Transform Claim Rule Wizard, select **Pass Through or Filter an Incoming Claim** from hello drop-down and click **Next**.</span></span>
   <span data-ttu-id="79154-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span><span class="sxs-lookup"><span data-stu-id="79154-137">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)</span></span>
6. <span data-ttu-id="79154-138">Dans hello boîte suivant tooClaim nom de la règle, nommez votre règle.</span><span class="sxs-lookup"><span data-stu-id="79154-138">In hello box next tooClaim rule name, give your rule a name.</span></span> <span data-ttu-id="79154-139">Par exemple : InsideCorpNet.</span><span class="sxs-lookup"><span data-stu-id="79154-139">For example: InsideCorpNet.</span></span>
7. <span data-ttu-id="79154-140">À partir de la liste déroulante de hello, tooIncoming suivant le type de revendication, sélectionnez **à l’intérieur d’un réseau d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="79154-140">From hello drop-down, next tooIncoming claim type, select **Inside Corporate Network**.</span></span>
   <span data-ttu-id="79154-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span><span class="sxs-lookup"><span data-stu-id="79154-141">![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)</span></span>
8. <span data-ttu-id="79154-142">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="79154-142">Click **Finish**.</span></span>
9. <span data-ttu-id="79154-143">Sous Règles de transformation d’émission, cliquez sur **Ajouter une règle**.</span><span class="sxs-lookup"><span data-stu-id="79154-143">On Issuance Transform Rules, click **Add Rule**.</span></span>
10. <span data-ttu-id="79154-144">On hello ajouter un Assistant de règle de revendication transformer, sélectionnez **envoyer des revendications à l’aide d’une règle personnalisée** dans hello de liste déroulante, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="79154-144">On hello Add Transform Claim Rule Wizard, select **Send Claims Using a Custom Rule** from hello drop-down and click **Next**.</span></span>
11. <span data-ttu-id="79154-145">Dans la zone hello sous le nom de règle de revendication : entrez *signé l’utilisateurs conserver dans*.</span><span class="sxs-lookup"><span data-stu-id="79154-145">In hello box under Claim rule name: enter *Keep Users Signed In*.</span></span>
12. <span data-ttu-id="79154-146">Dans la zone de règle personnalisée hello, entrez :</span><span class="sxs-lookup"><span data-stu-id="79154-146">In hello Custom rule box, enter:</span></span>

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. <span data-ttu-id="79154-148">Cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="79154-148">Click **Finish**.</span></span>
14. <span data-ttu-id="79154-149">Cliquez sur **Apply**.</span><span class="sxs-lookup"><span data-stu-id="79154-149">Click **Apply**.</span></span>
15. <span data-ttu-id="79154-150">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="79154-150">Click **Ok**.</span></span>
16. <span data-ttu-id="79154-151">Fermez Gestion AD FS.</span><span class="sxs-lookup"><span data-stu-id="79154-151">Close AD FS Management.</span></span>

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a><span data-ttu-id="79154-152">Configuration d'adresses IP de confiance Azure Multi-Factor Authentication avec des utilisateurs fédérés</span><span class="sxs-lookup"><span data-stu-id="79154-152">Configure Azure Multi-Factor Authentication Trusted IPs with Federated Users</span></span>
<span data-ttu-id="79154-153">Maintenant que les revendications hello sont en place, nous pouvons configurer des adresses IP approuvées.</span><span class="sxs-lookup"><span data-stu-id="79154-153">Now that hello claims are in place, we can configure trusted IPs.</span></span>

1. <span data-ttu-id="79154-154">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="79154-154">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="79154-155">Sur hello gauche, cliquez sur **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="79154-155">On hello left, click **Active Directory**.</span></span>
3. <span data-ttu-id="79154-156">Sous répertoire, sélectionnez le répertoire de hello où vous souhaitez tooset des adresses IP approuvées.</span><span class="sxs-lookup"><span data-stu-id="79154-156">Under Directory, select hello directory where you want tooset up trusted IPs.</span></span>
4. <span data-ttu-id="79154-157">Dans hello active que vous avez sélectionné, cliquez sur **configurer**.</span><span class="sxs-lookup"><span data-stu-id="79154-157">On hello Directory you have selected, click **Configure**.</span></span>
5. <span data-ttu-id="79154-158">Dans la section de l’authentification multifacteur hello, cliquez sur **gérer les paramètres de service**.</span><span class="sxs-lookup"><span data-stu-id="79154-158">In hello multi-factor authentication section, click **Manage service settings**.</span></span>
6. <span data-ttu-id="79154-159">Dans la page Paramètres du Service hello, sous adresses IP approuvées, sélectionnez **ignorer multi-factor-authentication pour les demandes des utilisateurs fédérés sur mon intranet**.</span><span class="sxs-lookup"><span data-stu-id="79154-159">On hello Service Settings page, under trusted IPs, select **Skip multi-factor-authentication for requests from federated users on my intranet**.</span></span>  

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. <span data-ttu-id="79154-161">Cliquez sur **save**.</span><span class="sxs-lookup"><span data-stu-id="79154-161">Click **save**.</span></span>
8. <span data-ttu-id="79154-162">Une fois les mises à jour hello ont été appliquées, cliquez sur **fermer**.</span><span class="sxs-lookup"><span data-stu-id="79154-162">Once hello updates have been applied, click **close**.</span></span>

<span data-ttu-id="79154-163">Et voilà !</span><span class="sxs-lookup"><span data-stu-id="79154-163">That’s it!</span></span> <span data-ttu-id="79154-164">À ce stade, les utilisateurs fédérés Office 365 ne doivent avoir toouse l’authentification Multifacteur lorsqu’une revendication provient d’intranet en dehors de l’entreprise hello.</span><span class="sxs-lookup"><span data-stu-id="79154-164">At this point, federated Office 365 users should only have toouse MFA when a claim originates from outside hello corporate intranet.</span></span>
