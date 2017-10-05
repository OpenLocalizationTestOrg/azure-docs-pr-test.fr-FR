---
title: "Manuel d’Azure Active Directory Identity Protection | Microsoft Docs"
description: "Découvrez comment Azure AD Identity Protection vous permet de limiter la capacité d’un cybercriminel à exploiter une identité ou un appareil compromis et de sécuriser une identité ou un appareil déjà identifié comme potentiellement ou effectivement compromis."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestion d’applications, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 60836abf-f0e9-459d-b344-8e06b8341d25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 2ecd07faed785fa6aa179ac1cca35a70d965e1dc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-playbook"></a><span data-ttu-id="31876-104">Manuel d’Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="31876-104">Azure Active Directory Identity Protection playbook</span></span>
<span data-ttu-id="31876-105">Ce manuel vous aide à :</span><span class="sxs-lookup"><span data-stu-id="31876-105">This playbook helps you to:</span></span>

* <span data-ttu-id="31876-106">Remplir les données dans l’environnement d’Identity Protection en simulant par des vulnérabilités et des événements à risque</span><span class="sxs-lookup"><span data-stu-id="31876-106">Populate data in the Identity Protection environment by simulating risk events and vulnerabilities</span></span>
* <span data-ttu-id="31876-107">Définir des stratégies d’accès conditionnel en fonction des risques et tester l’impact de ces stratégies</span><span class="sxs-lookup"><span data-stu-id="31876-107">Set up risk-based conditional access policies and test the impact of these policies</span></span>

## <a name="simulating-risk-events"></a><span data-ttu-id="31876-108">Simulation des événements à risque</span><span class="sxs-lookup"><span data-stu-id="31876-108">Simulating Risk Events</span></span>
<span data-ttu-id="31876-109">Cette section vous fournit les étapes requises pour simuler des types d’événements à risque suivants (le niveau de difficulté est indiqué entre parenthèses) :</span><span class="sxs-lookup"><span data-stu-id="31876-109">This section provides you with steps for simulating the following risk event types:</span></span>

* <span data-ttu-id="31876-110">Connexions depuis des adresses IP anonymes (facile)</span><span class="sxs-lookup"><span data-stu-id="31876-110">Sign-ins from anonymous IP addresses (easy)</span></span>
* <span data-ttu-id="31876-111">Connexions depuis des emplacements non connus (moyen)</span><span class="sxs-lookup"><span data-stu-id="31876-111">Sign-ins from unfamiliar locations (moderate)</span></span>
* <span data-ttu-id="31876-112">Voyage impossible vers des emplacements inhabituels (difficile)</span><span class="sxs-lookup"><span data-stu-id="31876-112">Impossible travel to atypical locations (difficult)</span></span>

<span data-ttu-id="31876-113">Les autres événements à risque ne peuvent pas être simulés de manière sécurisée.</span><span class="sxs-lookup"><span data-stu-id="31876-113">Other risk events cannot be simulated in a secure manner.</span></span>

### <a name="sign-ins-from-anonymous-ip-addresses"></a><span data-ttu-id="31876-114">Connexions depuis des adresses IP anonymes</span><span class="sxs-lookup"><span data-stu-id="31876-114">Sign-ins from anonymous IP addresses</span></span>
<span data-ttu-id="31876-115">Ce type d’événement à risque signale les utilisateurs qui se sont connectés depuis une adresse IP ayant été identifiée comme l’adresse IP d’un proxy anonyme.</span><span class="sxs-lookup"><span data-stu-id="31876-115">This risk event type identifies users who have successfully signed in from an IP address that has been identified as an anonymous proxy IP address.</span></span> <span data-ttu-id="31876-116">Ces proxys sont utilisés par des individus souhaitant masquer l’adresse IP de leur appareil et peuvent être utilisés dans un but malveillant.</span><span class="sxs-lookup"><span data-stu-id="31876-116">These proxies are used by people who want to hide their device’s IP address and may be used for malicious intent.</span></span>

<span data-ttu-id="31876-117">**Pour simuler une connexion depuis une adresse IP anonyme, procédez comme suit**:</span><span class="sxs-lookup"><span data-stu-id="31876-117">**To simulate a sign-in from an anonymous IP, perform the following steps**:</span></span>

1. <span data-ttu-id="31876-118">Téléchargez le [navigateur Tor](https://www.torproject.org/projects/torbrowser.html.en).</span><span class="sxs-lookup"><span data-stu-id="31876-118">Download the [Tor Browser](https://www.torproject.org/projects/torbrowser.html.en).</span></span>
2. <span data-ttu-id="31876-119">À l’aide du navigateur Tor, accédez à [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="31876-119">Using the Tor Browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>   
3. <span data-ttu-id="31876-120">Entrez les informations d’identification du compte que vous souhaitez voir apparaître dans le rapport **Connexions depuis des adresses IP anonymes** .</span><span class="sxs-lookup"><span data-stu-id="31876-120">Enter the credentials of the account you want to appear in the **Sign-ins from anonymous IP addresses** report.</span></span>

<span data-ttu-id="31876-121">La connexion s’affiche dans le tableau de bord d’Identity Protection dans un délai de 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="31876-121">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span> 

### <a name="sign-ins-from-unfamiliar-locations"></a><span data-ttu-id="31876-122">Connexions depuis des emplacements non connus</span><span class="sxs-lookup"><span data-stu-id="31876-122">Sign-ins from unfamiliar locations</span></span>
<span data-ttu-id="31876-123">Le risque lié aux emplacements non connus est déterminé à l’aide d’un mécanisme d’évaluation de connexion en temps réel qui prend en compte les emplacements de connexion passés (IP, latitude/longitude et NSA) pour déterminer les emplacements non connus/nouveaux.</span><span class="sxs-lookup"><span data-stu-id="31876-123">The unfamiliar locations risk is a real-time sign-in evaluation mechanism that considers past sign-in locations (IP, Latitude / Longitude and ASN) to determine new / unfamiliar locations.</span></span> <span data-ttu-id="31876-124">Le système stocke les adresses IP, la latitude/longitude et les NSA précédents d’un utilisateur et considère ces emplacements comme connus.</span><span class="sxs-lookup"><span data-stu-id="31876-124">The system stores previous IPs, Latitude / Longitude, and ASNs of a user and considers these to be familiar locations.</span></span> <span data-ttu-id="31876-125">Un emplacement de connexion est considéré comme non connu si l’emplacement de connexion ne correspond à aucun emplacement connu existant.</span><span class="sxs-lookup"><span data-stu-id="31876-125">A sign-in location is considered unfamiliar if the sign-in location does not match any of the existing familiar locations.</span></span>

<span data-ttu-id="31876-126">Azure Active Directory Identity Protection :</span><span class="sxs-lookup"><span data-stu-id="31876-126">Azure Active Directory Identity Protection:</span></span>  

* <span data-ttu-id="31876-127">présente une période d’apprentissage initiale de 14 jours, durant laquelle il ne signale pas les nouveaux emplacements en tant qu’emplacements non connus.</span><span class="sxs-lookup"><span data-stu-id="31876-127">has an initial learning period of 14 days during which it does not flag any new locations as unfamiliar locations.</span></span>
* <span data-ttu-id="31876-128">ignore les connexions depuis les appareils connus et les emplacements géographiquement proches d’un emplacement connu existant.</span><span class="sxs-lookup"><span data-stu-id="31876-128">ignores sign-ins from familiar devices and locations that are geographically close to an existing familiar location.</span></span>

<span data-ttu-id="31876-129">Pour simuler des emplacements non connus, vous devez vous connecter depuis un emplacement et un appareil depuis lesquels le compte ne s’est jamais connecté.</span><span class="sxs-lookup"><span data-stu-id="31876-129">To simulate unfamiliar locations, you have to sign in from a location and device that the account has not signed in from before.</span></span> 

<span data-ttu-id="31876-130">**Pour simuler une connexion depuis un emplacement non connu, procédez comme suit**:</span><span class="sxs-lookup"><span data-stu-id="31876-130">**To simulate a sign-in from an unfamiliar location, perform the following steps**:</span></span>

1. <span data-ttu-id="31876-131">Choisissez un compte qui présente un historique de connexion d’au moins 14 jours.</span><span class="sxs-lookup"><span data-stu-id="31876-131">Choose an account that has at least a 14-day sign-in history.</span></span> 
2. <span data-ttu-id="31876-132">Effectuez ensuite l’une ou l’autre de ces étapes :</span><span class="sxs-lookup"><span data-stu-id="31876-132">Do either:</span></span>
   
   <span data-ttu-id="31876-133">a.</span><span class="sxs-lookup"><span data-stu-id="31876-133">a.</span></span> <span data-ttu-id="31876-134">Tout en utilisant un VPN, accédez à [https://myapps.microsoft.com](https://myapps.microsoft.com) et entrez les informations d’identification du compte pour lequel vous souhaitez simuler cet événement à risque.</span><span class="sxs-lookup"><span data-stu-id="31876-134">While using a VPN, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com) and enter the credentials of the account you want to simulate the risk event for.</span></span>
   
   <span data-ttu-id="31876-135">b.</span><span class="sxs-lookup"><span data-stu-id="31876-135">b.</span></span> <span data-ttu-id="31876-136">Demandez à un collaborateur se trouvant à un emplacement différent de se connecter à l’aide des informations d’identification du compte (non recommandé).</span><span class="sxs-lookup"><span data-stu-id="31876-136">Ask an associate in a different location to sign in using the account’s credentials (not recommended).</span></span>

<span data-ttu-id="31876-137">La connexion s’affiche dans le tableau de bord d’Identity Protection dans un délai de 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="31876-137">The sign-in will show up on the Identity Protection dashboard within 5 minutes.</span></span>

### <a name="impossible-travel-to-atypical-location"></a><span data-ttu-id="31876-138">Voyage impossible vers des emplacements inhabituels</span><span class="sxs-lookup"><span data-stu-id="31876-138">Impossible travel to atypical location</span></span>
<span data-ttu-id="31876-139">La simulation de la condition de voyage impossible est difficile, car l’algorithme utilise l’apprentissage automatique pour éliminer les faux positifs, tels que le voyage impossible depuis des appareils connus ou les connexions depuis des VPN utilisés par d’autres utilisateurs du répertoire.</span><span class="sxs-lookup"><span data-stu-id="31876-139">Simulating the impossible travel condition is difficult because the algorithm uses machine learning to weed out false-positives such as impossible travel from familiar devices, or sign-ins from VPNs that are used by other users in the directory.</span></span> <span data-ttu-id="31876-140">De plus, l’algorithme requiert un historique de connexion de 3 à 14 jours pour l’utilisateur avant de commencer à générer des événements à risque.</span><span class="sxs-lookup"><span data-stu-id="31876-140">Additionally, the algorithm requires a sign-in history of 3 to 14 days for the user before it begins generating risk events.</span></span>

<span data-ttu-id="31876-141">**Pour simuler un voyage impossible vers des emplacements inhabituels, procédez comme suit**:</span><span class="sxs-lookup"><span data-stu-id="31876-141">**To simulate an impossible travel to atypical location, perform the following steps**:</span></span>

1. <span data-ttu-id="31876-142">À l’aide de votre navigateur standard, accédez à [https://myapps.microsoft.com](https://myapps.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="31876-142">Using your standard browser, navigate to [https://myapps.microsoft.com](https://myapps.microsoft.com).</span></span>  
2. <span data-ttu-id="31876-143">Entrez les informations d’identification du compte pour lequel vous souhaitez générer cet événement à risque.</span><span class="sxs-lookup"><span data-stu-id="31876-143">Enter the credentials of the account you want to generate an impossible travel risk event for.</span></span>
3. <span data-ttu-id="31876-144">Changez votre agent utilisateur.</span><span class="sxs-lookup"><span data-stu-id="31876-144">Change your user agent.</span></span> <span data-ttu-id="31876-145">Vous pouvez changer l’agent utilisateur depuis les outils de développement dans Internet Explorer ou à l’aide d’un module complémentaire de sélecteur d’agents utilisateur dans Firefox ou Chrome.</span><span class="sxs-lookup"><span data-stu-id="31876-145">You can change user agent in Internet Explorer from Developer Tools, or change your user agent in Firefox or Chrome using a user-agent switcher add-on.</span></span>
4. <span data-ttu-id="31876-146">Changez votre adresse IP.</span><span class="sxs-lookup"><span data-stu-id="31876-146">Change your IP address.</span></span> <span data-ttu-id="31876-147">Vous pouvez changer votre adresse IP en utilisant un VPN, un module complémentaire Tor ou en créant une nouvelle machine au sein d’Azure dans un autre centre de données.</span><span class="sxs-lookup"><span data-stu-id="31876-147">You can change your IP address by using a VPN, a Tor add-on, or spinning up a new machine in Azure in a different data center.</span></span>
5. <span data-ttu-id="31876-148">Connectez-vous à [https://myapps.microsoft.com](https://myapps.microsoft.com) à l’aide des mêmes informations d’identification que précédemment et dans un délai de quelques minutes seulement après la connexion précédente.</span><span class="sxs-lookup"><span data-stu-id="31876-148">Sign-in to [https://myapps.microsoft.com](https://myapps.microsoft.com) using the same credentials as before and within a few minutes after the previous sign-in.</span></span>

<span data-ttu-id="31876-149">La connexion s’affiche dans le tableau de bord d’Identity Protection dans un délai de 2 à 4 heures.</span><span class="sxs-lookup"><span data-stu-id="31876-149">The sign-in will show up in the Identity Protection dashboard within 2-4 hours.</span></span><br>
<span data-ttu-id="31876-150">En raison des modèles d’apprentissage automatique complexes impliqués, il se peut qu’elle ne soit pas détectée.</span><span class="sxs-lookup"><span data-stu-id="31876-150">Because of the complex machine learning models involved, there is a chance it will not get picked up.</span></span><br> <span data-ttu-id="31876-151">Il peut être judicieux de répéter ces étapes pour plusieurs comptes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31876-151">You might want to replicate these steps for multiple Azure AD accounts.</span></span>

## <a name="simulating-vulnerabilities"></a><span data-ttu-id="31876-152">Simulation de vulnérabilités</span><span class="sxs-lookup"><span data-stu-id="31876-152">Simulating vulnerabilities</span></span>
<span data-ttu-id="31876-153">Les vulnérabilités sont des points faibles exploitables par une personne malveillante au sein de votre environnement Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31876-153">Vulnerabilities are weaknesses in an Azure AD environment that can be exploited by a bad actor.</span></span> <span data-ttu-id="31876-154">Actuellement, Azure AD Identity Protection présente trois types de vulnérabilités tirant parti d’autres fonctionnalités d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="31876-154">Currently 3 types of vulnerabilities are surfaced in Azure AD Identity Protection that leverage other features of Azure AD.</span></span> <span data-ttu-id="31876-155">Ces vulnérabilités s’affichent automatiquement dans le tableau de bord d’Identity Protection dès lors que ces fonctionnalités sont configurées.</span><span class="sxs-lookup"><span data-stu-id="31876-155">These Vulnerabilities will be displayed on the Identity Protection dashboard automatically once these features are set up.</span></span>

* <span data-ttu-id="31876-156">Azure AD [Multi-Factor Authentication ?](../multi-factor-authentication/multi-factor-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="31876-156">Azure AD [Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)</span></span>
* <span data-ttu-id="31876-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="31876-157">Azure AD [Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).</span></span>
* <span data-ttu-id="31876-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span><span class="sxs-lookup"><span data-stu-id="31876-158">Azure AD [Privileged Identity Management](active-directory-privileged-identity-management-configure.md).</span></span> 

## <a name="user-compromise-risk"></a><span data-ttu-id="31876-159">Risque de compromission de l’utilisateur</span><span class="sxs-lookup"><span data-stu-id="31876-159">User compromise risk</span></span>
<span data-ttu-id="31876-160">**Pour tester le risque de compromission de l’utilisateur, procédez comme suit**:</span><span class="sxs-lookup"><span data-stu-id="31876-160">**To test User compromise risk, perform the following steps**:</span></span>

1. <span data-ttu-id="31876-161">Connectez-vous à [https://portal.azure.com](https://portal.azure.com) à l’aide des informations d’identification d’administrateur général pour votre client.</span><span class="sxs-lookup"><span data-stu-id="31876-161">Sign-in to [https://portal.azure.com](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="31876-162">Accédez à **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="31876-162">Navigate to **Identity Protection**.</span></span> 
3. <span data-ttu-id="31876-163">Dans le panneau principal **d’Azure AD Identity Protection**, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="31876-163">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="31876-164">Dans le panneau **Paramètres du portail**, sous **Règles de sécurité**, cliquez sur **Risque de compromission de l’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="31876-164">On the **Portal Settings** blade, under **Security rules**, click **User compromise risk**.</span></span> 
5. <span data-ttu-id="31876-165">Dans le panneau **Risque à la connexion**, désactivez l’option **Activer la règle**, puis cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="31876-165">On the **Sign in Risk** blade, turn **Enable rule** off, and then click **Save** settings.</span></span>
6. <span data-ttu-id="31876-166">Pour un compte d’utilisateur donné, simulez un événement à risque lié à des emplacements non connus ou à une adresse IP anonyme.</span><span class="sxs-lookup"><span data-stu-id="31876-166">For a given user account, simulate an unfamiliar locations or anonymous IP risk event.</span></span> <span data-ttu-id="31876-167">Cela aura pour effet d’élever le niveau de risque de cet utilisateur à **Moyen**.</span><span class="sxs-lookup"><span data-stu-id="31876-167">This will elevate the user risk level for that user to **Medium**.</span></span>
7. <span data-ttu-id="31876-168">Patientez quelques minutes et vérifiez que le niveau de risque de votre utilisateur est défini sur **Moyen**.</span><span class="sxs-lookup"><span data-stu-id="31876-168">Wait a few minutes, and then verify that user level for your user is **Medium**.</span></span>
8. <span data-ttu-id="31876-169">Accédez au panneau **Paramètres du portail** .</span><span class="sxs-lookup"><span data-stu-id="31876-169">Go to the **Portal Settings** blade.</span></span>
9. <span data-ttu-id="31876-170">Dans le panneau **Risque de compromission de l’utilisateur**, sélectionnez **Oui** sous **Activer la règle**.</span><span class="sxs-lookup"><span data-stu-id="31876-170">On the **User Compromise Risk** blade, under **Enable rule**, select **On** .</span></span> 
10. <span data-ttu-id="31876-171">Sélectionnez l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="31876-171">Select one of the following options:</span></span>
    
    <span data-ttu-id="31876-172">a.</span><span class="sxs-lookup"><span data-stu-id="31876-172">a.</span></span> <span data-ttu-id="31876-173">Pour bloquer l’accès, sélectionnez **Moyen** sous **Bloquer la connexion**.</span><span class="sxs-lookup"><span data-stu-id="31876-173">To block, select **Medium** under **Block sign in**.</span></span>
    
    <span data-ttu-id="31876-174">b.</span><span class="sxs-lookup"><span data-stu-id="31876-174">b.</span></span> <span data-ttu-id="31876-175">Pour appliquer un changement de mot de passe sécurisé, sélectionnez **Moyen** sous **Exiger une authentification multifacteur**.</span><span class="sxs-lookup"><span data-stu-id="31876-175">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
11. <span data-ttu-id="31876-176">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="31876-176">Click **Save**.</span></span>
12. <span data-ttu-id="31876-177">Vous pouvez maintenant tester l’accès conditionnel en fonction des risques en vous connectant à l’aide d’un compte d’utilisateur présentant un niveau de risque élevé.</span><span class="sxs-lookup"><span data-stu-id="31876-177">You can now test risk-based conditional access by signing in using a user with an elevated risk level.</span></span> <span data-ttu-id="31876-178">Si le risque de l’utilisateur est défini sur Moyen, votre connexion sera bloquée ou vous serez obligé de changer votre mot de passe, selon la configuration de votre stratégie.</span><span class="sxs-lookup"><span data-stu-id="31876-178">If the user risk is Medium, depending on the configuration of your policy, your sign-in is be either blocked or you are forced to change your password.</span></span> 
    <br><br><span data-ttu-id="31876-179">
    ![Manuel de](./media/active-directory-identityprotection-playbook/201.png "manuel")
    </span><span class="sxs-lookup"><span data-stu-id="31876-179">
![Playbook](./media/active-directory-identityprotection-playbook/201.png "Playbook")
</span></span><br>

## <a name="sign-in-risk"></a><span data-ttu-id="31876-180">Risque à la connexion</span><span class="sxs-lookup"><span data-stu-id="31876-180">Sign-in risk</span></span>
<span data-ttu-id="31876-181">**Pour tester le risque à la connexion, procédez comme suit :**</span><span class="sxs-lookup"><span data-stu-id="31876-181">**To test a sign in risk, perform the following steps:**</span></span>

1. <span data-ttu-id="31876-182">Connectez-vous à [https://portal.azure.com ](https://portal.azure.com) à l’aide des informations d’identification d’administrateur général pour votre client.</span><span class="sxs-lookup"><span data-stu-id="31876-182">Sign-in to [https://portal.azure.com ](https://portal.azure.com) with global administrator credentials for your tenant.</span></span>
2. <span data-ttu-id="31876-183">Accédez à **Identity Protection**.</span><span class="sxs-lookup"><span data-stu-id="31876-183">Navigate to **Identity Protection**.</span></span>
3. <span data-ttu-id="31876-184">Dans le panneau principal **d’Azure AD Identity Protection**, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="31876-184">On the main **Azure AD Identity Protection** blade, click **Settings**.</span></span> 
4. <span data-ttu-id="31876-185">Dans le panneau **Paramètres du portail** panneau, sous **Règles de sécurité**, cliquez sur **Risque à la connexion**.</span><span class="sxs-lookup"><span data-stu-id="31876-185">On the **Portal Settings** blade, under **Security rules**, click **Sign in risk**.</span></span>
5. <span data-ttu-id="31876-186">Sur la ** risque de se connecter ** panneau, sélectionnez **sur** sous **activer règle**.</span><span class="sxs-lookup"><span data-stu-id="31876-186">On the **Sign in Risk **blade, select **On** under **Enable rule**.</span></span> 
6. <span data-ttu-id="31876-187">Sélectionnez l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="31876-187">Select one of the following options:</span></span>
   
   <span data-ttu-id="31876-188">a.</span><span class="sxs-lookup"><span data-stu-id="31876-188">a.</span></span> <span data-ttu-id="31876-189">Pour bloquer l’accès, sélectionnez **Moyen** sous **Bloquer la connexion**</span><span class="sxs-lookup"><span data-stu-id="31876-189">To block, select **Medium** under **Block sign in**</span></span>
   
   <span data-ttu-id="31876-190">b.</span><span class="sxs-lookup"><span data-stu-id="31876-190">b.</span></span> <span data-ttu-id="31876-191">Pour appliquer un changement de mot de passe sécurisé, sélectionnez **Moyen** sous **Exiger une authentification multifacteur**.</span><span class="sxs-lookup"><span data-stu-id="31876-191">To enforce secure password change, select **Medium** under **Require multi-factor authentication**.</span></span>
7. <span data-ttu-id="31876-192">Pour bloquer l’accès, sélectionnez Moyen sous Bloquer la connexion.</span><span class="sxs-lookup"><span data-stu-id="31876-192">To block, select Medium under Block sign in.</span></span>
8. <span data-ttu-id="31876-193">Pour appliquer l’authentification multifacteur, sélectionnez **Moyen** sous **Exiger une authentification multifacteur**.</span><span class="sxs-lookup"><span data-stu-id="31876-193">To enforce multi-factor authentication, select **Medium** under **Require multi-factor authentication**.</span></span>
9. <span data-ttu-id="31876-194">Cliquez sur **Save**(Enregistrer).</span><span class="sxs-lookup"><span data-stu-id="31876-194">Click on **Save**.</span></span>
10. <span data-ttu-id="31876-195">Vous pouvez maintenant tester l’accès conditionnel en fonction des risques en simulant les événements à risque liés à des emplacements inhabituels ou à des adresses IP anonymes, dont le risque est considéré comme **moyen** .</span><span class="sxs-lookup"><span data-stu-id="31876-195">You can now test risk-based conditional access by simulating the unfamiliar locations or anonymous IP risk events because they are both **Medium** risk events.</span></span>


<span data-ttu-id="31876-196">![Manuel](./media/active-directory-identityprotection-playbook/200.png "Manuel")</span><span class="sxs-lookup"><span data-stu-id="31876-196">![Playbook](./media/active-directory-identityprotection-playbook/200.png "Playbook")</span></span>


## <a name="see-also"></a><span data-ttu-id="31876-197">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="31876-197">See also</span></span>
* [<span data-ttu-id="31876-198">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="31876-198">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

