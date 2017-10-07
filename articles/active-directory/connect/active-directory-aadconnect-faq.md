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
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="bbb4a-103">Forum Aux Questions sur Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="bbb4a-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="bbb4a-104">Installation générale</span><span class="sxs-lookup"><span data-stu-id="bbb4a-104">General installation</span></span>
<span data-ttu-id="bbb4a-105">**Q : installation fonctionnera si hello un administrateur Global Azure AD a 2FA activé ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-105">**Q: Will installation work if hello Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="bbb4a-106">Hello des générations à partir de février 2016, cela est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-106">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="bbb4a-107">**Q : existe-t-il un moyen de tooinstall sans assistance Azure AD Connect ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-107">**Q: Is there a way tooinstall Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="bbb4a-108">Il est uniquement pris en charge tooinstall Azure AD Connect à l’aide de l’Assistant installation hello.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-108">It is only supported tooinstall Azure AD Connect using hello installation wizard.</span></span> <span data-ttu-id="bbb4a-109">Une installation automatique et silencieuse n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="bbb4a-110">**Q : Je possède une forêt dans laquelle un domaine ne peut pas être contacté. Comment installer Azure AD Connect ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="bbb4a-111">Hello des générations à partir de février 2016, cela est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-111">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="bbb4a-112">**Q : hello travail de l’agent d’intégrité de domaine Active Directory sur server core ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-112">**Q: Does hello AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="bbb4a-113">Oui.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-113">Yes.</span></span> <span data-ttu-id="bbb4a-114">Après avoir installé l’agent de hello, vous pouvez terminer le processus de l’inscription de hello à l’aide de hello suivant l’applet de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="bbb4a-114">After installing hello agent, you can complete hello registration process using hello following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="bbb4a-115">Réseau</span><span class="sxs-lookup"><span data-stu-id="bbb4a-115">Network</span></span>
<span data-ttu-id="bbb4a-116">**Q : je dispose d’un pare-feu, un périphérique réseau, ou quelque chose d’autre qui limite les connexions de durée maximale hello peut rester ouvert sur mon réseau. Quel doit être le seuil de délai côté client lors de l’utilisation d’Azure AD Connect ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-116">**Q: I have a firewall, network device, or something else that limits hello maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="bbb4a-117">Tous les logiciels de mise en réseau, périphériques physiques ou tout autre élément hello durée maximale de connexions peuvent ouvrir doit utiliser un seuil d’au moins 5 minutes (300 secondes) pour la connectivité entre les limites hello serveur sur lequel hello Azure AD Connect client est installé et Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-117">All networking software, physical devices, or anything else that limits hello maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between hello server where hello Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="bbb4a-118">Cela s’applique également des outils de synchronisation de Microsoft Identity tooall précédemment publiée.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-118">This also applies tooall previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="bbb4a-119">**Q : Les domaines avec un nom en une seule partie sont-ils pris en charge ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="bbb4a-120">Non, Azure AD Connect ne prend pas en charge les forêts/domaines locaux utilisant des noms de domaine en une seule partie.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="bbb4a-121">**Q : Les noms NetBios comportant un point sont-ils pris en charge ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="bbb4a-122">Non, Azure AD Connect ne prend pas en charge localement forêts/domaines où le nom NetBios hello contient un point «. » dans le nom de hello.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-122">No, Azure AD Connect does not support on-premises forests/domains where hello NetBios name contains a period "." in hello name.</span></span>

## <a name="federation"></a><span data-ttu-id="bbb4a-123">Fédération</span><span class="sxs-lookup"><span data-stu-id="bbb4a-123">Federation</span></span>
<span data-ttu-id="bbb4a-124">**Q : que faire si je reçois un message électronique qui me demande toorenew mon certificat Office 365**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-124">**Q: What do I do if I receive an email that asking me toorenew my Office 365 certificate**</span></span>  
<span data-ttu-id="bbb4a-125">Utilisez les instructions de hello qui sont décrite dans hello [renouveler les certificats](active-directory-aadconnect-o365-certs.md) rubrique sur la façon dont toorenew hello certificat.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-125">Use hello guidance that is outlined in hello [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how toorenew hello certificate.</span></span>

<span data-ttu-id="bbb4a-126">**Q : « Mettre à jour automatiquement la partie de confiance » est défini pour la partie de confiance Office 365. Dois-je tootake n’importe quelle action lorsque mon automatiquement le certificat de signature de jeton survole ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have tootake any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="bbb4a-127">Utilisez les instructions de hello qui sont décrite dans l’article de hello [renouveler les certificats](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="bbb4a-127">Use hello guidance that is outlined in hello article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="bbb4a-128">Environnement</span><span class="sxs-lookup"><span data-stu-id="bbb4a-128">Environment</span></span>
<span data-ttu-id="bbb4a-129">**Q : est-il pris en charge d’informatique toorename hello server après l’installation d’Azure AD Connect ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-129">**Q: Is it supported toorename hello server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="bbb4a-130">Non.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-130">No.</span></span> <span data-ttu-id="bbb4a-131">Modification du nom de serveur hello toonot de moteur de synchronisation de hello cause sera en mesure de tooconnect toohello base de données SQL et le service de hello ne sera pas en mesure de toostart.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-131">Changing hello server name will cause hello sync engine toonot be able tooconnect toohello SQL database and hello service will not be able toostart.</span></span>

## <a name="identity-data"></a><span data-ttu-id="bbb4a-132">Données d’identité</span><span class="sxs-lookup"><span data-stu-id="bbb4a-132">Identity data</span></span>
<span data-ttu-id="bbb4a-133">**Q : attribut de nom UPN (userPrincipalName) hello dans Azure AD ne correspond pas à hello UPN de local - pourquoi ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-133">**Q: hello UPN (userPrincipalName) attribute in Azure AD does not match hello on-prem UPN - why?**</span></span>  
<span data-ttu-id="bbb4a-134">Reportez-vous aux articles suivants :</span><span class="sxs-lookup"><span data-stu-id="bbb4a-134">See these articles:</span></span>

* [<span data-ttu-id="bbb4a-135">Les noms d’utilisateur ne correspondent pas dans Office 365, Azure ou Intune hello UPN local ou l’ID de connexion de remplacement</span><span class="sxs-lookup"><span data-stu-id="bbb4a-135">User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="bbb4a-136">Les modifications ne sont pas synchronisées par l’outil de synchronisation Azure Active Directory hello après avoir modifié hello UPN d’un toouse de compte d’utilisateur un autre domaine fédéré</span><span class="sxs-lookup"><span data-stu-id="bbb4a-136">Changes aren't synced by hello Azure Active Directory Sync tool after you change hello UPN of a user account toouse a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="bbb4a-137">Vous pouvez également configurer Azure AD tooallow hello synchronisation moteur tooupdate hello userPrincipalName comme décrit dans [fonctionnalités de service de synchronisation Azure AD Connect](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="bbb4a-137">You can also configure Azure AD tooallow hello sync engine tooupdate hello userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="bbb4a-138">**Q : est informatique pris en charge toosoft correspondance locale objets AD groupe/Contact avec les objets groupe contacter Azure Active Directory existants ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-138">**Q: Is it supported toosoft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="bbb4a-139">Non, cela n’est pas pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-139">No, this is currently not supported.</span></span>

<span data-ttu-id="bbb4a-140">**Q : est-il informatique pris en charge toomanually définie ImmutableId attribut sur Azure AD groupe/Contact existant objets toohard établit une correspondance avec local tooon objets AD groupe/Contact ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-140">**Q: Is it supported toomanually set ImmutableId attribute on existing Azure AD Group/Contact objects toohard match it tooon-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="bbb4a-141">Non, cela n’est pas pris en charge actuellement.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="bbb4a-142">Configuration personnalisée</span><span class="sxs-lookup"><span data-stu-id="bbb4a-142">Custom configuration</span></span>
<span data-ttu-id="bbb4a-143">**Q : où se trouvent les applets de commande PowerShell hello pour Azure AD Connect documentée ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-143">**Q: Where are hello PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="bbb4a-144">Avec l’exception hello d’applets de commande hello sur ce site, autres applets de commande PowerShell trouvés dans Azure AD Connect ne sont pas pris en charge par le client.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-144">With hello exception of hello cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="bbb4a-145">**Q : puis-je utiliser la fonctionnalité « Importation de serveur d’exportation serveur » trouvée dans *Synchronization Service Manager* configuration toomove entre les serveurs ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* toomove configuration between servers?**</span></span>  
<span data-ttu-id="bbb4a-146">Non.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-146">No.</span></span> <span data-ttu-id="bbb4a-147">Cette option ne récupérera pas tous les paramètres de configuration et ne doit pas être utilisée.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="bbb4a-148">À la place utilisez hello Assistant toocreate hello base de configuration sur le second serveur de hello et utiliser hello synchronisation règle éditeur toogenerate PowerShell scripts toomove toute règle personnalisée entre les serveurs.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-148">You should instead use hello wizard toocreate hello base configuration on hello second server and use hello sync rule editor toogenerate PowerShell scripts toomove any custom rule between servers.</span></span> <span data-ttu-id="bbb4a-149">Consultez la section [Migration « Swing »](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="bbb4a-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="bbb4a-150">**Q : les mots de passe peuvent être mis en cache pour la page de hello signe dans Azure et peut cela impossible, car il contient un élément input de mot de passe avec la saisie semi-automatique hello = attribut « false » ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-150">**Q: Can passwords be cached for hello Azure sign-in page and can this be prevented since it contains a password input element with hello autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="bbb4a-151">Actuellement, nous ne permettent pas de modification d’attributs HTML hello du champ de saisie du mot de passe hello, y compris la balise de la saisie semi-automatique hello.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-151">We currently do not support modifying hello HTML attributes of hello Password input field, including hello autocomplete tag.</span></span> <span data-ttu-id="bbb4a-152">Nous travaillons actuellement sur une fonctionnalité qui permet de code Javascript personnalisé qui vous permettra de tooadd n’importe quel champ de mot de passe toohello attribut.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-152">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="bbb4a-153">Cette fonctionnalité devrait être accessible courant 2017.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="bbb4a-154">**Q : sur hello Azure-page de connexion, les noms d’utilisateur pour les utilisateurs qui ont précédemment connecté sont affichés.  Est-il possible de désactiver ce comportement ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-154">**Q: On hello Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="bbb4a-155">Actuellement, nous ne permettent pas de modification d’attributs HTML hello de hello-page de connexion.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-155">We currently do not support modifying hello HTML attributes of hello sign-in page.</span></span> <span data-ttu-id="bbb4a-156">Nous travaillons actuellement sur une fonctionnalité qui permet de code Javascript personnalisé qui vous permettra de tooadd n’importe quel champ de mot de passe toohello attribut.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-156">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="bbb4a-157">Cette fonctionnalité devrait être accessible courant 2017.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="bbb4a-158">**Q : existe-t-il un moyen tooprevent sessions simultanées ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-158">**Q: Is there a way tooprevent concurrent sessions?**</span></span></br>
<span data-ttu-id="bbb4a-159">Non.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="bbb4a-160">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="bbb4a-160">Troubleshooting</span></span>
<span data-ttu-id="bbb4a-161">**Q : Comment puis-je obtenir de l’aide avec Azure AD Connect ?**</span><span class="sxs-lookup"><span data-stu-id="bbb4a-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="bbb4a-162">Rechercher hello Base de connaissances Microsoft (KB)</span><span class="sxs-lookup"><span data-stu-id="bbb4a-162">Search hello Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="bbb4a-163">Rechercher hello Base de connaissances Microsoft (KB) pour les problèmes de réparation toocommon solutions techniques sur la prise en charge d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-163">Search hello Microsoft Knowledge Base (KB) for technical solutions toocommon break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="bbb4a-164">Forums Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bbb4a-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="bbb4a-165">Vous pouvez rechercher et Parcourir pour technical questions et réponses à partir de la Communauté de hello ou demandez à votre propre question en cliquant sur [ici](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="bbb4a-165">You can search and browse for technical questions and answers from hello community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="bbb4a-166">Service clientèle Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="bbb4a-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="bbb4a-167">Utilisez cette prise en charge de tooget lien via hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="bbb4a-167">Use this link tooget support through hello Azure portal.</span></span>

