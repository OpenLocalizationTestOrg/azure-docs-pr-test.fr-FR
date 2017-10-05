---
title: "Azure Active Directory Connect : Forum Aux Questions | Microsoft Docs"
description: "Cette page comporte le Forum Aux Questions relatif à Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: fd5988b2d4170166902bb5cc39603d4a0f83be59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="7312c-103">Forum Aux Questions sur Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="7312c-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="7312c-104">Installation générale</span><span class="sxs-lookup"><span data-stu-id="7312c-104">General installation</span></span>
<span data-ttu-id="7312c-105">**Q : L’installation fonctionnera-t-elle si l’option 2FA est activée pour l’administrateur global AD Azure ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-105">**Q: Will installation work if the Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="7312c-106">Cela est pris en charge avec les builds de février 2016.</span><span class="sxs-lookup"><span data-stu-id="7312c-106">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="7312c-107">**Q : Existe-t-il une manière d’installer Azure AD Connect sans assistance ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-107">**Q: Is there a way to install Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="7312c-108">L’installation d’Azure AD Connect n’est possible qu’à partir de l’Assistant Installation.</span><span class="sxs-lookup"><span data-stu-id="7312c-108">It is only supported to install Azure AD Connect using the installation wizard.</span></span> <span data-ttu-id="7312c-109">Une installation automatique et silencieuse n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="7312c-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="7312c-110">**Q : Je possède une forêt dans laquelle un domaine ne peut pas être contacté. Comment installer Azure AD Connect ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="7312c-111">Cela est pris en charge avec les builds de février 2016.</span><span class="sxs-lookup"><span data-stu-id="7312c-111">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="7312c-112">**Q : L’agent AD DS Health fonctionne-t-il sur Server Core ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-112">**Q: Does the AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="7312c-113">Oui.</span><span class="sxs-lookup"><span data-stu-id="7312c-113">Yes.</span></span> <span data-ttu-id="7312c-114">Après avoir installé l’agent, vous pouvez terminer le processus d’inscription à l’aide de l’applet de commande PowerShell suivante :</span><span class="sxs-lookup"><span data-stu-id="7312c-114">After installing the agent, you can complete the registration process using the following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="7312c-115">Réseau</span><span class="sxs-lookup"><span data-stu-id="7312c-115">Network</span></span>
<span data-ttu-id="7312c-116">**Q : J’ai un pare-feu, un périphérique réseau ou autre chose qui limite la durée maximale pendant laquelle les connexions peuvent rester ouvertes sur mon réseau. Quel doit être le seuil de délai côté client lors de l’utilisation d’Azure AD Connect ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-116">**Q: I have a firewall, network device, or something else that limits the maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="7312c-117">Tous les logiciels réseau, périphériques physiques ou autres limitant la durée maximale pendant laquelle les connexions peuvent rester ouvertes doivent utiliser un seuil d'au moins 5 minutes (300 secondes) pour la connectivité entre le serveur où est installé le client Azure AD Connect et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7312c-117">All networking software, physical devices, or anything else that limits the maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between the server where the Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="7312c-118">Cela s'applique également à tous les outils de synchronisation de Microsoft Identity précédemment publiés.</span><span class="sxs-lookup"><span data-stu-id="7312c-118">This also applies to all previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="7312c-119">**Q : Les domaines avec un nom en une seule partie sont-ils pris en charge ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="7312c-120">Non, Azure AD Connect ne prend pas en charge les forêts/domaines locaux utilisant des noms de domaine en une seule partie.</span><span class="sxs-lookup"><span data-stu-id="7312c-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="7312c-121">**Q : Les noms NetBios comportant un point sont-ils pris en charge ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="7312c-122">Non, Azure AD Connect ne prend pas en charge les forêts/domaines locaux  dont le nom NetBios contient un point « . ».</span><span class="sxs-lookup"><span data-stu-id="7312c-122">No, Azure AD Connect does not support on-premises forests/domains where the NetBios name contains a period "." in the name.</span></span>

## <a name="federation"></a><span data-ttu-id="7312c-123">Fédération</span><span class="sxs-lookup"><span data-stu-id="7312c-123">Federation</span></span>
<span data-ttu-id="7312c-124">**Q : Que faire si je reçois un e-mail me demandant de renouveler mon certificat Office 365**</span><span class="sxs-lookup"><span data-stu-id="7312c-124">**Q: What do I do if I receive an email that asking me to renew my Office 365 certificate**</span></span>  
<span data-ttu-id="7312c-125">Suivez les instructions décrites dans la rubrique [Renouveler les certificats](active-directory-aadconnect-o365-certs.md) concernant le renouvellement du certificat.</span><span class="sxs-lookup"><span data-stu-id="7312c-125">Use the guidance that is outlined in the [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how to renew the certificate.</span></span>

<span data-ttu-id="7312c-126">**Q : « Mettre à jour automatiquement la partie de confiance » est défini pour la partie de confiance Office 365. Dois-je effectuer une action lorsque mon certificat de signature de jetons bascule automatiquement ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have to take any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="7312c-127">Utilisez les instructions décrites dans l’article [Renouveler les certificats](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="7312c-127">Use the guidance that is outlined in the article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="7312c-128">Environnement</span><span class="sxs-lookup"><span data-stu-id="7312c-128">Environment</span></span>
<span data-ttu-id="7312c-129">**Q : Est-il possible de renommer le serveur une fois qu’Azure AD Connect est installé ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-129">**Q: Is it supported to rename the server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="7312c-130">Non.</span><span class="sxs-lookup"><span data-stu-id="7312c-130">No.</span></span> <span data-ttu-id="7312c-131">La modification du nom du serveur empêche le moteur de synchronisation de se connecter à la base de données SQL et le service de démarrer.</span><span class="sxs-lookup"><span data-stu-id="7312c-131">Changing the server name will cause the sync engine to not be able to connect to the SQL database and the service will not be able to start.</span></span>

## <a name="identity-data"></a><span data-ttu-id="7312c-132">Données d’identité</span><span class="sxs-lookup"><span data-stu-id="7312c-132">Identity data</span></span>
<span data-ttu-id="7312c-133">**Q : L’attribut UPN (userPrincipalName) dans Azure AD ne correspond pas à l’UPN local. Pourquoi ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-133">**Q: The UPN (userPrincipalName) attribute in Azure AD does not match the on-prem UPN - why?**</span></span>  
<span data-ttu-id="7312c-134">Reportez-vous aux articles suivants :</span><span class="sxs-lookup"><span data-stu-id="7312c-134">See these articles:</span></span>

* [<span data-ttu-id="7312c-135">Les noms d’utilisateur dans Office 365, Azure ou Intune ne correspondent pas à l’UPN local ou à l’ID de connexion secondaire</span><span class="sxs-lookup"><span data-stu-id="7312c-135">User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="7312c-136">Les modifications ne sont pas synchronisées par l’outil de synchronisation Azure Active Directory une fois que vous avez modifié l’UPN d’un compte utilisateur afin qu’il utilise un autre domaine fédéré</span><span class="sxs-lookup"><span data-stu-id="7312c-136">Changes aren't synced by the Azure Active Directory Sync tool after you change the UPN of a user account to use a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="7312c-137">Vous pouvez également configurer Azure AD pour permettre au moteur de synchronisation de mettre à jour userPrincipalName comme décrit dans [fonctionnalités du service de synchronisation Azure AD Connect](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="7312c-137">You can also configure Azure AD to allow the sync engine to update the userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="7312c-138">**Q : Est-ce que la correspondance approximative des objets Groupe/Contact AD locaux avec les objets Azure AD Groupe/Contact existants est prise en charge ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-138">**Q: Is it supported to soft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="7312c-139">Non, cela n’est pas pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="7312c-139">No, this is currently not supported.</span></span>

<span data-ttu-id="7312c-140">**Q : Est-il possible de définir manuellement l’attribut ImmutableId sur des objets Groupe/Contact Azure AD existants pour la mise en correspondance exacte avec les objets Groupe/Contact locaux ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-140">**Q: Is it supported to manually set ImmutableId attribute on existing Azure AD Group/Contact objects to hard match it to on-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="7312c-141">Non, cela n’est pas pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="7312c-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="7312c-142">Configuration personnalisée</span><span class="sxs-lookup"><span data-stu-id="7312c-142">Custom configuration</span></span>
<span data-ttu-id="7312c-143">**Q : Où réside la documentation sur les applets de commande PowerShell pour Azure Active Directory ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-143">**Q: Where are the PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="7312c-144">À l’exception des applets de commande décrites sur ce site, les autres applets de commande PowerShell disponibles dans Azure AD Connect ne sont pas prises en charge par le client.</span><span class="sxs-lookup"><span data-stu-id="7312c-144">With the exception of the cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="7312c-145">**Q : Puis-je utiliser « Exportation serveur/importation serveur » dans *Synchronization Service Manager* pour déplacer la configuration entre des serveurs ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* to move configuration between servers?**</span></span>  
<span data-ttu-id="7312c-146">Non.</span><span class="sxs-lookup"><span data-stu-id="7312c-146">No.</span></span> <span data-ttu-id="7312c-147">Cette option ne récupérera pas tous les paramètres de configuration et ne doit pas être utilisée.</span><span class="sxs-lookup"><span data-stu-id="7312c-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="7312c-148">Vous devez plutôt utiliser l’Assistant pour créer la configuration de base sur le deuxième serveur et utiliser l’éditeur de règles de synchronisation pour générer des scripts PowerShell afin de déplacer une règle personnalisée entre les serveurs.</span><span class="sxs-lookup"><span data-stu-id="7312c-148">You should instead use the wizard to create the base configuration on the second server and use the sync rule editor to generate PowerShell scripts to move any custom rule between servers.</span></span> <span data-ttu-id="7312c-149">Consultez la section [Migration « Swing »](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="7312c-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="7312c-150">**Q : Les mots de passe peuvent-ils être mis en cache pour la page de connexion Azure, et est-il possible d’empêcher cela, étant donné que la page contient un élément d’entrée de mot de passe avec l’attribut autocomplete = "false" ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-150">**Q: Can passwords be cached for the Azure sign-in page and can this be prevented since it contains a password input element with the autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="7312c-151">Pour l’instant, nous ne prenons pas en charge la modification des attributs HTML du champ d’entrée de mot de passe, et notamment de la balise « autocomplete ».</span><span class="sxs-lookup"><span data-stu-id="7312c-151">We currently do not support modifying the HTML attributes of the Password input field, including the autocomplete tag.</span></span> <span data-ttu-id="7312c-152">Nous travaillons actuellement à l’élaboration d’une fonctionnalité d’autorisation d’un code Javascript personnalisé qui vous permettra d’ajouter n’importe quel attribut au champ du mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7312c-152">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="7312c-153">Cette fonctionnalité devrait être accessible courant 2017.</span><span class="sxs-lookup"><span data-stu-id="7312c-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="7312c-154">**Q : La page de connexion Azure affiche les noms d’utilisateur des utilisateurs qui se sont déjà connectés avec succès.  Est-il possible de désactiver ce comportement ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-154">**Q: On the Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="7312c-155">Pour l’instant, nous ne prenons pas en charge la modification des attributs HTML de la page de connexion.</span><span class="sxs-lookup"><span data-stu-id="7312c-155">We currently do not support modifying the HTML attributes of the sign-in page.</span></span> <span data-ttu-id="7312c-156">Nous travaillons actuellement à l’élaboration d’une fonctionnalité d’autorisation d’un code Javascript personnalisé qui vous permettra d’ajouter n’importe quel attribut au champ du mot de passe.</span><span class="sxs-lookup"><span data-stu-id="7312c-156">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="7312c-157">Cette fonctionnalité devrait être accessible courant 2017.</span><span class="sxs-lookup"><span data-stu-id="7312c-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="7312c-158">**Q : Existe-t-il un moyen d’empêcher les sessions simultanées ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-158">**Q: Is there a way to prevent concurrent sessions?**</span></span></br>
<span data-ttu-id="7312c-159">Non.</span><span class="sxs-lookup"><span data-stu-id="7312c-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="7312c-160">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="7312c-160">Troubleshooting</span></span>
<span data-ttu-id="7312c-161">**Q : Comment puis-je obtenir de l’aide avec Azure AD Connect ?**</span><span class="sxs-lookup"><span data-stu-id="7312c-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="7312c-162">Recherche dans la Base de connaissances Microsoft (KB)</span><span class="sxs-lookup"><span data-stu-id="7312c-162">Search the Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="7312c-163">Recherchez dans la Base de connaissances Microsoft (KB) des solutions techniques aux problèmes courants couverts par la garantie de réparation et d’assistance, relatifs à la prise en charge d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="7312c-163">Search the Microsoft Knowledge Base (KB) for technical solutions to common break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="7312c-164">Forums Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7312c-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="7312c-165">Vous pouvez naviguer et rechercher des questions et des réponses techniques de la communauté ou poser votre question en cliquant [ici](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="7312c-165">You can search and browse for technical questions and answers from the community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="7312c-166">Service clientèle Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="7312c-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="7312c-167">Cliquez sur ce lien pour bénéficier du support par le biais du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7312c-167">Use this link to get support through the Azure portal.</span></span>

