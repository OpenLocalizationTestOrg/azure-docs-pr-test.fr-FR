---
title: aaaAzure AD connecter plusieurs domaines
description: "Ce document décrit la définition et la configuration de plusieurs domaines de premier niveau avec O365 et Azure AD."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 5595fb2f-2131-4304-8a31-c52559128ea4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 91d87875ceacee4e34f132938e4bb0294fb954e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a><span data-ttu-id="264bc-103">Prise en charge de plusieurs domaines pour la fédération avec Azure AD</span><span class="sxs-lookup"><span data-stu-id="264bc-103">Multiple Domain Support for Federating with Azure AD</span></span>
<span data-ttu-id="264bc-104">Hello documentation suivante fournit des conseils sur la façon de toouse plusieurs domaines de premier niveau et sous-domaines lors de la fédération avec Office 365 ou Azure AD de domaines.</span><span class="sxs-lookup"><span data-stu-id="264bc-104">hello following documentation provides guidance on how toouse multiple top-level domains and sub-domains when federating with Office 365 or Azure AD domains.</span></span>

## <a name="multiple-top-level-domain-support"></a><span data-ttu-id="264bc-105">Prise en charge de plusieurs domaines de niveau supérieur</span><span class="sxs-lookup"><span data-stu-id="264bc-105">Multiple top-level domain support</span></span>
<span data-ttu-id="264bc-106">La fédération de plusieurs domaines de niveau supérieur avec Azure AD nécessite une configuration supplémentaire qui n’est pas requise lors de la fédération avec un domaine de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="264bc-106">Federating multiple, top-level domains with Azure AD requires some additional configuration that is not required when federating with one top-level domain.</span></span>

<span data-ttu-id="264bc-107">Lorsqu’un domaine est fédéré avec Azure AD, plusieurs propriétés sont définies sur le domaine hello dans Azure.</span><span class="sxs-lookup"><span data-stu-id="264bc-107">When a domain is federated with Azure AD, several properties are set on hello domain in Azure.</span></span>  <span data-ttu-id="264bc-108">L’une des plus importantes est IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="264bc-108">One important one is IssuerUri.</span></span>  <span data-ttu-id="264bc-109">Il s’agit d’un URI qui est utilisé par Azure AD tooidentify domaine hello hello jetons est associé.</span><span class="sxs-lookup"><span data-stu-id="264bc-109">This is a URI that is used by Azure AD tooidentify hello domain that hello token is associated with.</span></span>  <span data-ttu-id="264bc-110">Hello URI n’a pas besoin tooresolve tooanything, mais il doit être un URI valide.</span><span class="sxs-lookup"><span data-stu-id="264bc-110">hello URI doesn’t need tooresolve tooanything but it must be a valid URI.</span></span>  <span data-ttu-id="264bc-111">Par défaut, AD Azure définit cette valeur toohello d’identificateur hello du service de fédération dans votre site AD FS configuration.</span><span class="sxs-lookup"><span data-stu-id="264bc-111">By default, Azure AD sets this toohello value of hello federation service identifier in your on-premises AD FS configuration.</span></span>

> [!NOTE]
> <span data-ttu-id="264bc-112">Identificateur du service de fédération Hello est un URI qui identifie de façon unique un service de fédération.</span><span class="sxs-lookup"><span data-stu-id="264bc-112">hello federation service identifier is a URI that uniquely identifies a federation service.</span></span>  <span data-ttu-id="264bc-113">service de fédération Hello est une instance d’AD FS qui fonctionne en tant que service de jeton de sécurité hello.</span><span class="sxs-lookup"><span data-stu-id="264bc-113">hello federation service is an instance of AD FS that functions as hello security token service.</span></span> 
> 
> 

<span data-ttu-id="264bc-114">Vous pouvez afficher IssuerUri à l’aide de commande PowerShell de hello `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span><span class="sxs-lookup"><span data-stu-id="264bc-114">You can vew IssuerUri by using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`.</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="264bc-116">Un problème se pose quand nous souhaitons tooadd plusieurs domaines de niveau supérieur.</span><span class="sxs-lookup"><span data-stu-id="264bc-116">A problem arises when we want tooadd more than one top-level domain.</span></span>  <span data-ttu-id="264bc-117">Par exemple, supposons que vous avez configuré la fédération entre Azure AD et votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="264bc-117">For example, let's say you have setup federation between Azure AD and your on-premises environment.</span></span>  <span data-ttu-id="264bc-118">Pour ce document, j’utilise bmcontoso.com.  J’ai ajouté un second domaine de premier niveau, bmfabrikam.com.</span><span class="sxs-lookup"><span data-stu-id="264bc-118">For this document I am using bmcontoso.com.  Now I have added a second, top-level domain, bmfabrikam.com.</span></span>

![Domaines](./media/active-directory-multiple-domains/domains.png)

<span data-ttu-id="264bc-120">Lorsque vous essayez de tooconvert notre toobe de domaine bmfabrikam.com fédéré, nous recevoir une erreur.</span><span class="sxs-lookup"><span data-stu-id="264bc-120">When we attempt tooconvert our bmfabrikam.com domain toobe federated, we receive an error.</span></span>  <span data-ttu-id="264bc-121">Hello en fait, Azure AD a une contrainte qui n’autorise pas hello hello de toohave IssuerUri propriété même valeur pour plusieurs domaines.</span><span class="sxs-lookup"><span data-stu-id="264bc-121">hello reason for this is, Azure AD has a constraint that does not allow hello IssuerUri property toohave hello same value for more than one domain.</span></span>  

![Erreur de fédération](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a><span data-ttu-id="264bc-123">Paramètre SupportMultipleDomain</span><span class="sxs-lookup"><span data-stu-id="264bc-123">SupportMultipleDomain Parameter</span></span>
<span data-ttu-id="264bc-124">tooworkaround, nous devons tooadd un IssuerUri différent qui peut être effectuée à l’aide de hello `-SupportMultipleDomain` paramètre.</span><span class="sxs-lookup"><span data-stu-id="264bc-124">tooworkaround this, we need tooadd a different IssuerUri which can be done by using hello `-SupportMultipleDomain` parameter.</span></span>  <span data-ttu-id="264bc-125">Ce paramètre est utilisé avec hello suivant d’applets de commande :</span><span class="sxs-lookup"><span data-stu-id="264bc-125">This parameter is used with hello following cmdlets:</span></span>

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

<span data-ttu-id="264bc-126">Ce paramètre permet de configurer hello IssuerUri afin qu’il soit basé sur le nom hello du domaine de hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="264bc-126">This parameter makes Azure AD configure hello IssuerUri so that it is based on hello name of hello domain.</span></span>  <span data-ttu-id="264bc-127">Ceci sera unique au sein des annuaires dans Azure AD.</span><span class="sxs-lookup"><span data-stu-id="264bc-127">This will be unique across directories in Azure AD.</span></span>  <span data-ttu-id="264bc-128">À l’aide du paramètre hello permet de toocomplete de commande PowerShell hello avec succès.</span><span class="sxs-lookup"><span data-stu-id="264bc-128">Using hello parameter allows hello PowerShell command toocomplete successfully.</span></span>

![Erreur de fédération](./media/active-directory-multiple-domains/convert.png)

<span data-ttu-id="264bc-130">Affichage des paramètres hello de notre nouveau domaine bmfabrikam.com vous hello éléments suivants sont affichés :</span><span class="sxs-lookup"><span data-stu-id="264bc-130">Looking at hello settings of our new bmfabrikam.com domain you can see hello following:</span></span>

![Erreur de fédération](./media/active-directory-multiple-domains/settings.png)

<span data-ttu-id="264bc-132">Notez que `-SupportMultipleDomain` ne change pas hello autres points de terminaison qui sont toujours configuré service de fédération toopoint tooour sur adfs.bmcontoso.com.</span><span class="sxs-lookup"><span data-stu-id="264bc-132">Note that `-SupportMultipleDomain` does not change hello other endpoints which are still configured toopoint tooour federation service on adfs.bmcontoso.com.</span></span>

<span data-ttu-id="264bc-133">Une autre chose que `-SupportMultipleDomain` est consiste à s’assurer que le système de hello AD FS inclut valeur d’émetteur correct hello dans les jetons émis pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="264bc-133">Another thing that `-SupportMultipleDomain` does is that it ensures that hello AD FS system includes hello proper Issuer value in tokens issued for Azure AD.</span></span> <span data-ttu-id="264bc-134">Pour ce faire prendre la partie consacrée au domaine des utilisateurs de hello UPN hello et la définition de cette propriété en tant que domaine hello Bonjour IssuerUri, c'est-à-dire https://{upn suffixe} / adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="264bc-134">It does this by taking hello domain portion of hello users UPN and setting this as hello domain in hello IssuerUri, i.e. https://{upn suffix}/adfs/services/trust.</span></span> 

<span data-ttu-id="264bc-135">Par conséquent, lors de l’authentification tooAzure AD ou Office 365, élément IssuerUri hello hello jeton d’utilisateur est toolocate utilisé hello domaine Azure AD.</span><span class="sxs-lookup"><span data-stu-id="264bc-135">Thus during authentication tooAzure AD or Office 365, hello IssuerUri element in hello user’s token is used toolocate hello domain in Azure AD.</span></span>  <span data-ttu-id="264bc-136">Si une correspondance ne peut pas être trouvée hello l’authentification échoue.</span><span class="sxs-lookup"><span data-stu-id="264bc-136">If a match cannot be found hello authentication will fail.</span></span> 

<span data-ttu-id="264bc-137">Par exemple, si un utilisateur du nom UPN est bsimon@bmcontoso.com, élément de IssuerUri hello dans les problèmes AD FS jeton hello définira toohttp://bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="264bc-137">For example, if a user’s UPN is bsimon@bmcontoso.com, hello IssuerUri element in hello token AD FS issues will be set toohttp://bmcontoso.com/adfs/services/trust.</span></span> <span data-ttu-id="264bc-138">Cela correspondre configuration d’Azure AD hello, et l’authentification réussira.</span><span class="sxs-lookup"><span data-stu-id="264bc-138">This will match hello Azure AD configuration, and authentication will succeed.</span></span>

<span data-ttu-id="264bc-139">Hello Voici la règle de revendication personnalisée hello qui implémente cette logique :</span><span class="sxs-lookup"><span data-stu-id="264bc-139">hello following is hello customized claim rule that implements this logic:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> <span data-ttu-id="264bc-140">Dans l’ordre toouse hello SupportMultipleDomain - commutateur lors de la tentative de tooadd nouvelle ou convertir déjà ajouté des domaines, vous devez toohave le programme d’installation de votre approbation fédérée de toosupport leur origine.</span><span class="sxs-lookup"><span data-stu-id="264bc-140">In order toouse hello -SupportMultipleDomain switch when attempting tooadd new or convert already added domains, you need toohave setup your federated trust toosupport them originally.</span></span>  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a><span data-ttu-id="264bc-141">Comment tooupdate hello approbation entre AD FS et Azure AD</span><span class="sxs-lookup"><span data-stu-id="264bc-141">How tooupdate hello trust between AD FS and Azure AD</span></span>
<span data-ttu-id="264bc-142">Si vous n’avez pas paramétré hello fédéré une approbation entre AD FS et de votre instance d’Azure AD, vous devrez peut-être toore-créer cette approbation.</span><span class="sxs-lookup"><span data-stu-id="264bc-142">If you did not setup hello federated trust between AD FS and your instance of Azure AD, you may need toore-create this trust.</span></span>  <span data-ttu-id="264bc-143">Effet, lorsqu’il est à l’origine le programme d’installation sans hello `-SupportMultipleDomain` paramètre hello IssuerUri est définie avec la valeur par défaut de hello.</span><span class="sxs-lookup"><span data-stu-id="264bc-143">This is because, when it is originally setup without hello `-SupportMultipleDomain` parameter, hello IssuerUri is set with hello default value.</span></span>  <span data-ttu-id="264bc-144">Bonjour, la capture d’écran ci-dessous, vous pouvez voir hello IssuerUri a la valeur toohttps://adfs.bmcontoso.com/adfs/services/trust.</span><span class="sxs-lookup"><span data-stu-id="264bc-144">In hello screenshot below you can see hello IssuerUri is set toohttps://adfs.bmcontoso.com/adfs/services/trust.</span></span>

<span data-ttu-id="264bc-145">C’est le cas présent, si nous avez ajouté un nouveau domaine dans le portail de hello Azure AD, puis tooconvert à l’aide de `Convert-MsolDomaintoFederated -DomainName <your domain>`, nous obtenons hello l’erreur suivante.</span><span class="sxs-lookup"><span data-stu-id="264bc-145">So now, if we have successfully added an new domain in hello Azure AD portal and then attempt tooconvert it using `Convert-MsolDomaintoFederated -DomainName <your domain>`, we get hello following error.</span></span>

![Erreur de fédération](./media/active-directory-multiple-domains/trust1.png)

<span data-ttu-id="264bc-147">Si vous essayez de tooadd hello `-SupportMultipleDomain` commutateur que nous recevrons hello l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="264bc-147">If you try tooadd hello `-SupportMultipleDomain` switch we will receive hello following error:</span></span>

![Erreur de fédération](./media/active-directory-multiple-domains/trust2.png)

<span data-ttu-id="264bc-149">La tentative de simplement toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` sur hello domaine d’origine également entraîne une erreur.</span><span class="sxs-lookup"><span data-stu-id="264bc-149">Simply trying toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` on hello original domain will also result in an error.</span></span>

![Erreur de fédération](./media/active-directory-multiple-domains/trust3.png)

<span data-ttu-id="264bc-151">Utilisez les étapes de hello ci-dessous tooadd un domaine de niveau supérieur supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="264bc-151">Use hello steps below tooadd an additional top-level domain.</span></span>  <span data-ttu-id="264bc-152">Si vous avez déjà ajouté un domaine et que vous n’avez pas utilisé hello `-SupportMultipleDomain` paramètre commencent étapes hello pour suppression et de mise à jour de votre domaine d’origine.</span><span class="sxs-lookup"><span data-stu-id="264bc-152">If you have already added a domain and did not use hello `-SupportMultipleDomain` parameter start with hello steps for removing and updating your original domain.</span></span>  <span data-ttu-id="264bc-153">Si vous n’avez pas ajouté un domaine de premier niveau encore vous pouvez démarrer avec étapes hello pour l’ajout d’un domaine à l’aide de PowerShell d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="264bc-153">If you have not added a top-level domain yet you can start with hello steps for adding a domain using PowerShell of Azure AD Connect.</span></span>

<span data-ttu-id="264bc-154">Hello suivant les étapes tooremove hello Microsoft Online approbation et mettre à jour de votre domaine d’origine.</span><span class="sxs-lookup"><span data-stu-id="264bc-154">Use hello following steps tooremove hello Microsoft Online trust and update your original domain.</span></span>

1. <span data-ttu-id="264bc-155">Sur votre serveur de fédération AD FS, ouvrez **Gestion AD FS.**</span><span class="sxs-lookup"><span data-stu-id="264bc-155">On your AD FS federation server open **AD FS Management.**</span></span> 
2. <span data-ttu-id="264bc-156">Sur hello gauche, développez **relations d’approbation** et **approbations de partie de confiance**</span><span class="sxs-lookup"><span data-stu-id="264bc-156">On hello left, expand **Trust Relationships** and **Relying Party Trusts**</span></span>
3. <span data-ttu-id="264bc-157">Sur hello droite, supprimez hello **plateforme d’identité Microsoft Office 365** entrée.</span><span class="sxs-lookup"><span data-stu-id="264bc-157">On hello right, delete hello **Microsoft Office 365 Identity Platform** entry.</span></span>
   <span data-ttu-id="264bc-158">![Supprimer Microsoft en ligne](./media/active-directory-multiple-domains/trust4.png)</span><span class="sxs-lookup"><span data-stu-id="264bc-158">![Remove Microsoft Online](./media/active-directory-multiple-domains/trust4.png)</span></span>
4. <span data-ttu-id="264bc-159">Sur un ordinateur qui a [Azure Module Active Directory pour Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installé exécutez hello suivante : `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="264bc-159">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
5. <span data-ttu-id="264bc-160">Entrez le nom d’utilisateur hello et un mot de passe d’un administrateur général pour le domaine Azure AD de hello avec que fédération</span><span class="sxs-lookup"><span data-stu-id="264bc-160">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
6. <span data-ttu-id="264bc-161">Dans PowerShell, entrez `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="264bc-161">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
7. <span data-ttu-id="264bc-162">Dans PowerShell, entrez `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span><span class="sxs-lookup"><span data-stu-id="264bc-162">In PowerShell enter `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.</span></span>  <span data-ttu-id="264bc-163">Il s’agit pour le domaine d’origine de hello.</span><span class="sxs-lookup"><span data-stu-id="264bc-163">This is for hello original domain.</span></span>  <span data-ttu-id="264bc-164">À l’aide de hello au-dessus de domaines, qu'il serait :`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span><span class="sxs-lookup"><span data-stu-id="264bc-164">So using hello above domains it would be:  `Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`</span></span>

<span data-ttu-id="264bc-165">Utilisez hello suivant les étapes tooadd hello nouveau domaine de niveau supérieur à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="264bc-165">Use hello following steps tooadd hello new top-level domain using PowerShell</span></span>

1. <span data-ttu-id="264bc-166">Sur un ordinateur qui a [Azure Module Active Directory pour Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installé exécutez hello suivante : `$cred=Get-Credential`.</span><span class="sxs-lookup"><span data-stu-id="264bc-166">On a machine that has [Azure Active Directory Module for Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installed on it run hello following: `$cred=Get-Credential`.</span></span>  
2. <span data-ttu-id="264bc-167">Entrez le nom d’utilisateur hello et un mot de passe d’un administrateur général pour le domaine Azure AD de hello avec que fédération</span><span class="sxs-lookup"><span data-stu-id="264bc-167">Enter hello username and password of a global administrator for hello Azure AD domain you are federating with</span></span>
3. <span data-ttu-id="264bc-168">Dans PowerShell, entrez `Connect-MsolService -Credential $cred`</span><span class="sxs-lookup"><span data-stu-id="264bc-168">In PowerShell enter `Connect-MsolService -Credential $cred`</span></span>
4. <span data-ttu-id="264bc-169">Dans PowerShell, entrez `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span><span class="sxs-lookup"><span data-stu-id="264bc-169">In PowerShell enter `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`</span></span>

<span data-ttu-id="264bc-170">Utilisez hello suivant les étapes tooadd hello nouveau domaine de niveau supérieur à l’aide d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="264bc-170">Use hello following steps tooadd hello new top-level domain using Azure AD Connect.</span></span>

1. <span data-ttu-id="264bc-171">Lancez Azure AD Connect à partir du bureau de hello ou le menu Démarrer</span><span class="sxs-lookup"><span data-stu-id="264bc-171">Launch Azure AD Connect from hello desktop or start menu</span></span>
2. <span data-ttu-id="264bc-172">Choisissez « Ajouter un domaine Azure AD supplémentaire » ![Ajouter un domaine Azure AD supplémentaire](./media/active-directory-multiple-domains/add1.png)</span><span class="sxs-lookup"><span data-stu-id="264bc-172">Choose “Add an additional Azure AD Domain” ![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add1.png)</span></span>
3. <span data-ttu-id="264bc-173">Entrez votre informations d’identification Azure AD et Active Directory</span><span class="sxs-lookup"><span data-stu-id="264bc-173">Enter your Azure AD and Active Directory credentials</span></span>
4. <span data-ttu-id="264bc-174">Sélectionnez hello deuxième domaine vous souhaitez tooconfigure pour la fédération.</span><span class="sxs-lookup"><span data-stu-id="264bc-174">Select hello second domain you wish tooconfigure for federation.</span></span>
   <span data-ttu-id="264bc-175">![Ajouter un domaine Azure AD supplémentaire](./media/active-directory-multiple-domains/add2.png)</span><span class="sxs-lookup"><span data-stu-id="264bc-175">![Add an additional Azure AD domain](./media/active-directory-multiple-domains/add2.png)</span></span>
5. <span data-ttu-id="264bc-176">Cliquez sur Installer</span><span class="sxs-lookup"><span data-stu-id="264bc-176">Click Install</span></span>

### <a name="verify-hello-new-top-level-domain"></a><span data-ttu-id="264bc-177">Vérifiez que le nouveau domaine de niveau supérieur hello</span><span class="sxs-lookup"><span data-stu-id="264bc-177">Verify hello new top-level domain</span></span>
<span data-ttu-id="264bc-178">À l’aide de commande PowerShell de hello `Get-MsolDomainFederationSettings -DomainName <your domain>`que vous pouvez afficher hello mis à jour IssuerUri.</span><span class="sxs-lookup"><span data-stu-id="264bc-178">By using hello PowerShell command `Get-MsolDomainFederationSettings -DomainName <your domain>`you can view hello updated IssuerUri.</span></span>  <span data-ttu-id="264bc-179">capture d’écran Hello ci-dessous montre les paramètres de fédération hello ont été mis à jour sur nos http://bmcontoso.com/adfs/services/trust domaine d’origine</span><span class="sxs-lookup"><span data-stu-id="264bc-179">hello screenshot below shows hello federation settings were updated on our original domain http://bmcontoso.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

<span data-ttu-id="264bc-181">Et toohttps://bmfabrikam.com/adfs/services/trust a été défini à hello IssuerUri sur notre nouveau domaine</span><span class="sxs-lookup"><span data-stu-id="264bc-181">And hello IssuerUri on our new domain has been set toohttps://bmfabrikam.com/adfs/services/trust</span></span>

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a><span data-ttu-id="264bc-183">Prise en charge des sous-domaines</span><span class="sxs-lookup"><span data-stu-id="264bc-183">Support for Sub-domains</span></span>
<span data-ttu-id="264bc-184">Lorsque vous ajoutez un sous-domaine, géré de domaines en raison de hello façon Azure AD, elle héritera des paramètres hello du parent de hello.</span><span class="sxs-lookup"><span data-stu-id="264bc-184">When you add a sub-domain, because of hello way Azure AD handled domains, it will inherit hello settings of hello parent.</span></span>  <span data-ttu-id="264bc-185">Cela signifie que hello IssuerUri doit parents de hello toomatch.</span><span class="sxs-lookup"><span data-stu-id="264bc-185">This means that hello IssuerUri needs toomatch hello parents.</span></span>

<span data-ttu-id="264bc-186">Donc, supposons que j’ai bmcontoso.com et que j’ajoute ensuite corp.bmcontoso.com.  Cela signifie que hello IssuerUri pour un utilisateur à partir de corp.bmcontoso.com devez toobe **http://bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="264bc-186">So lets say for example that I have bmcontoso.com and then add corp.bmcontoso.com.  This means that hello IssuerUri for a user from corp.bmcontoso.com will need toobe **http://bmcontoso.com/adfs/services/trust.**</span></span>  <span data-ttu-id="264bc-187">Toutefois, les règles standard hello implémentée ci-dessus pour Azure AD, génère un jeton avec un émetteur en tant que **http://corp.bmcontoso.com/adfs/services/trust.**</span><span class="sxs-lookup"><span data-stu-id="264bc-187">However hello standard rule implemented above for Azure AD, will generate a token with an issuer as **http://corp.bmcontoso.com/adfs/services/trust.**</span></span> <span data-ttu-id="264bc-188">qui ne correspondra pas à la valeur requise du domaine hello et l’authentification échoue.</span><span class="sxs-lookup"><span data-stu-id="264bc-188">which will not match hello domain's required value and authentication will fail.</span></span>

### <a name="how-tooenable-support-for-sub-domains"></a><span data-ttu-id="264bc-189">Comment tooenable prennent en charge pour les sous-domaines</span><span class="sxs-lookup"><span data-stu-id="264bc-189">How tooenable support for sub-domains</span></span>
<span data-ttu-id="264bc-190">AD FS de confiance pour Microsoft Online toowork ordre autour de cette hello doit toobe mis à jour.</span><span class="sxs-lookup"><span data-stu-id="264bc-190">In order toowork around this hello AD FS relying party trust for Microsoft Online needs toobe updated.</span></span>  <span data-ttu-id="264bc-191">toodo, vous devez configurer une règle de revendication personnalisée afin qu’il supprime les sous-domaines de suffixe UPN de l’utilisateur hello lors de la construction de valeur d’émetteur hello personnalisé.</span><span class="sxs-lookup"><span data-stu-id="264bc-191">toodo this, you must configure a custom claim rule so that it strips off any sub-domains from hello user’s UPN suffix when constructing hello custom Issuer value.</span></span> 

<span data-ttu-id="264bc-192">Hello suivant revendication sera procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="264bc-192">hello following claim will do this:</span></span>

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
<span data-ttu-id="264bc-193">dernier numéro de Hello dans l’expression régulière de hello définie hello les domaines parents combien il existe dans votre domaine racine.</span><span class="sxs-lookup"><span data-stu-id="264bc-193">hello last number in hello regular expression set hello how many parent domains there is in your root domain.</span></span> <span data-ttu-id="264bc-194">Dans le cas présent, j’ai bmcontoso.com. Deux domaines parents sont donc nécessaires.</span><span class="sxs-lookup"><span data-stu-id="264bc-194">Here i have bmcontoso.com so two parent domains are necessary.</span></span> <span data-ttu-id="264bc-195">Si trois parent domaines ont été toobe conservé (par exemple : corp.bmcontoso.com), puis le nombre de hello aurait été trois.</span><span class="sxs-lookup"><span data-stu-id="264bc-195">If three parent domains were toobe kept (i.e.: corp.bmcontoso.com), then hello number would have been three.</span></span> <span data-ttu-id="264bc-196">Éventuellement, une plage peut être indiquée, correspondance de hello est toujours effectuée maximum hello toomatch domaines.</span><span class="sxs-lookup"><span data-stu-id="264bc-196">Eventualy a range can be indicated, hello match will always be made toomatch hello maximum of domains.</span></span> <span data-ttu-id="264bc-197">« {2,3} » correspond à deux domaines toothree (c'est-à-dire : bmfabrikam.com et corp.bmcontoso.com).</span><span class="sxs-lookup"><span data-stu-id="264bc-197">"{2,3}" will match two toothree domains (i.e.: bmfabrikam.com and corp.bmcontoso.com).</span></span>

<span data-ttu-id="264bc-198">Utilisez hello suivant les étapes tooadd un sous-domaines toosupport de revendication personnalisée.</span><span class="sxs-lookup"><span data-stu-id="264bc-198">Use hello following steps tooadd a custom claim toosupport sub-domains.</span></span>

1. <span data-ttu-id="264bc-199">Ouvrez Gestion AD FS</span><span class="sxs-lookup"><span data-stu-id="264bc-199">Open AD FS Management</span></span>
2. <span data-ttu-id="264bc-200">Cliquez avec le bouton droit sur approbation de partie de confiance en ligne Microsoft hello et choisir les règles de revendication de modifier</span><span class="sxs-lookup"><span data-stu-id="264bc-200">Right click hello Microsoft Online RP trust and choose Edit Claim rules</span></span>
3. <span data-ttu-id="264bc-201">Sélectionnez la règle de revendication troisième hello et remplacez ![demande de modification](./media/active-directory-multiple-domains/sub1.png)</span><span class="sxs-lookup"><span data-stu-id="264bc-201">Select hello third claim rule, and replace ![Edit claim](./media/active-directory-multiple-domains/sub1.png)</span></span>
4. <span data-ttu-id="264bc-202">Remplacez la revendication en cours hello :</span><span class="sxs-lookup"><span data-stu-id="264bc-202">Replace hello current claim:</span></span>
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Remplacer la revendication](./media/active-directory-multiple-domains/sub2.png)

5. <span data-ttu-id="264bc-204">Cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="264bc-204">Click Ok.</span></span>  <span data-ttu-id="264bc-205">Cliquez sur Appliquer.</span><span class="sxs-lookup"><span data-stu-id="264bc-205">Click Apply.</span></span>  <span data-ttu-id="264bc-206">Cliquez sur OK.</span><span class="sxs-lookup"><span data-stu-id="264bc-206">Click Ok.</span></span>  <span data-ttu-id="264bc-207">Fermez Gestion AD FS.</span><span class="sxs-lookup"><span data-stu-id="264bc-207">Close AD FS Management.</span></span>

