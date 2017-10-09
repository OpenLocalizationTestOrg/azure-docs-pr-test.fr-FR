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
# <a name="multiple-domain-support-for-federating-with-azure-ad"></a>Prise en charge de plusieurs domaines pour la fédération avec Azure AD
Hello documentation suivante fournit des conseils sur la façon de toouse plusieurs domaines de premier niveau et sous-domaines lors de la fédération avec Office 365 ou Azure AD de domaines.

## <a name="multiple-top-level-domain-support"></a>Prise en charge de plusieurs domaines de niveau supérieur
La fédération de plusieurs domaines de niveau supérieur avec Azure AD nécessite une configuration supplémentaire qui n’est pas requise lors de la fédération avec un domaine de niveau supérieur.

Lorsqu’un domaine est fédéré avec Azure AD, plusieurs propriétés sont définies sur le domaine hello dans Azure.  L’une des plus importantes est IssuerUri.  Il s’agit d’un URI qui est utilisé par Azure AD tooidentify domaine hello hello jetons est associé.  Hello URI n’a pas besoin tooresolve tooanything, mais il doit être un URI valide.  Par défaut, AD Azure définit cette valeur toohello d’identificateur hello du service de fédération dans votre site AD FS configuration.

> [!NOTE]
> Identificateur du service de fédération Hello est un URI qui identifie de façon unique un service de fédération.  service de fédération Hello est une instance d’AD FS qui fonctionne en tant que service de jeton de sécurité hello. 
> 
> 

Vous pouvez afficher IssuerUri à l’aide de commande PowerShell de hello `Get-MsolDomainFederationSettings -DomainName <your domain>`.

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Un problème se pose quand nous souhaitons tooadd plusieurs domaines de niveau supérieur.  Par exemple, supposons que vous avez configuré la fédération entre Azure AD et votre environnement local.  Pour ce document, j’utilise bmcontoso.com.  J’ai ajouté un second domaine de premier niveau, bmfabrikam.com.

![Domaines](./media/active-directory-multiple-domains/domains.png)

Lorsque vous essayez de tooconvert notre toobe de domaine bmfabrikam.com fédéré, nous recevoir une erreur.  Hello en fait, Azure AD a une contrainte qui n’autorise pas hello hello de toohave IssuerUri propriété même valeur pour plusieurs domaines.  

![Erreur de fédération](./media/active-directory-multiple-domains/error.png)

### <a name="supportmultipledomain-parameter"></a>Paramètre SupportMultipleDomain
tooworkaround, nous devons tooadd un IssuerUri différent qui peut être effectuée à l’aide de hello `-SupportMultipleDomain` paramètre.  Ce paramètre est utilisé avec hello suivant d’applets de commande :

* `New-MsolFederatedDomain`
* `Convert-MsolDomaintoFederated`
* `Update-MsolFederatedDomain`

Ce paramètre permet de configurer hello IssuerUri afin qu’il soit basé sur le nom hello du domaine de hello Azure AD.  Ceci sera unique au sein des annuaires dans Azure AD.  À l’aide du paramètre hello permet de toocomplete de commande PowerShell hello avec succès.

![Erreur de fédération](./media/active-directory-multiple-domains/convert.png)

Affichage des paramètres hello de notre nouveau domaine bmfabrikam.com vous hello éléments suivants sont affichés :

![Erreur de fédération](./media/active-directory-multiple-domains/settings.png)

Notez que `-SupportMultipleDomain` ne change pas hello autres points de terminaison qui sont toujours configuré service de fédération toopoint tooour sur adfs.bmcontoso.com.

Une autre chose que `-SupportMultipleDomain` est consiste à s’assurer que le système de hello AD FS inclut valeur d’émetteur correct hello dans les jetons émis pour Azure AD. Pour ce faire prendre la partie consacrée au domaine des utilisateurs de hello UPN hello et la définition de cette propriété en tant que domaine hello Bonjour IssuerUri, c'est-à-dire https://{upn suffixe} / adfs/services/trust. 

Par conséquent, lors de l’authentification tooAzure AD ou Office 365, élément IssuerUri hello hello jeton d’utilisateur est toolocate utilisé hello domaine Azure AD.  Si une correspondance ne peut pas être trouvée hello l’authentification échoue. 

Par exemple, si un utilisateur du nom UPN est bsimon@bmcontoso.com, élément de IssuerUri hello dans les problèmes AD FS jeton hello définira toohttp://bmcontoso.com/adfs/services/trust. Cela correspondre configuration d’Azure AD hello, et l’authentification réussira.

Hello Voici la règle de revendication personnalisée hello qui implémente cette logique :

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)", "http://${domain}/adfs/services/trust/"));


> [!IMPORTANT]
> Dans l’ordre toouse hello SupportMultipleDomain - commutateur lors de la tentative de tooadd nouvelle ou convertir déjà ajouté des domaines, vous devez toohave le programme d’installation de votre approbation fédérée de toosupport leur origine.  
> 
> 

## <a name="how-tooupdate-hello-trust-between-ad-fs-and-azure-ad"></a>Comment tooupdate hello approbation entre AD FS et Azure AD
Si vous n’avez pas paramétré hello fédéré une approbation entre AD FS et de votre instance d’Azure AD, vous devrez peut-être toore-créer cette approbation.  Effet, lorsqu’il est à l’origine le programme d’installation sans hello `-SupportMultipleDomain` paramètre hello IssuerUri est définie avec la valeur par défaut de hello.  Bonjour, la capture d’écran ci-dessous, vous pouvez voir hello IssuerUri a la valeur toohttps://adfs.bmcontoso.com/adfs/services/trust.

C’est le cas présent, si nous avez ajouté un nouveau domaine dans le portail de hello Azure AD, puis tooconvert à l’aide de `Convert-MsolDomaintoFederated -DomainName <your domain>`, nous obtenons hello l’erreur suivante.

![Erreur de fédération](./media/active-directory-multiple-domains/trust1.png)

Si vous essayez de tooadd hello `-SupportMultipleDomain` commutateur que nous recevrons hello l’erreur suivante :

![Erreur de fédération](./media/active-directory-multiple-domains/trust2.png)

La tentative de simplement toorun `Update-MsolFederatedDomain -DomainName <your domain> -SupportMultipleDomain` sur hello domaine d’origine également entraîne une erreur.

![Erreur de fédération](./media/active-directory-multiple-domains/trust3.png)

Utilisez les étapes de hello ci-dessous tooadd un domaine de niveau supérieur supplémentaire.  Si vous avez déjà ajouté un domaine et que vous n’avez pas utilisé hello `-SupportMultipleDomain` paramètre commencent étapes hello pour suppression et de mise à jour de votre domaine d’origine.  Si vous n’avez pas ajouté un domaine de premier niveau encore vous pouvez démarrer avec étapes hello pour l’ajout d’un domaine à l’aide de PowerShell d’Azure AD Connect.

Hello suivant les étapes tooremove hello Microsoft Online approbation et mettre à jour de votre domaine d’origine.

1. Sur votre serveur de fédération AD FS, ouvrez **Gestion AD FS.** 
2. Sur hello gauche, développez **relations d’approbation** et **approbations de partie de confiance**
3. Sur hello droite, supprimez hello **plateforme d’identité Microsoft Office 365** entrée.
   ![Supprimer Microsoft en ligne](./media/active-directory-multiple-domains/trust4.png)
4. Sur un ordinateur qui a [Azure Module Active Directory pour Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installé exécutez hello suivante : `$cred=Get-Credential`.  
5. Entrez le nom d’utilisateur hello et un mot de passe d’un administrateur général pour le domaine Azure AD de hello avec que fédération
6. Dans PowerShell, entrez `Connect-MsolService -Credential $cred`
7. Dans PowerShell, entrez `Update-MSOLFederatedDomain -DomainName <Federated Domain Name> -SupportMultipleDomain`.  Il s’agit pour le domaine d’origine de hello.  À l’aide de hello au-dessus de domaines, qu'il serait :`Update-MsolFederatedDomain -DomainName bmcontoso.com -SupportMultipleDomain`

Utilisez hello suivant les étapes tooadd hello nouveau domaine de niveau supérieur à l’aide de PowerShell

1. Sur un ordinateur qui a [Azure Module Active Directory pour Windows PowerShell](https://msdn.microsoft.com/library/azure/jj151815.aspx) installé exécutez hello suivante : `$cred=Get-Credential`.  
2. Entrez le nom d’utilisateur hello et un mot de passe d’un administrateur général pour le domaine Azure AD de hello avec que fédération
3. Dans PowerShell, entrez `Connect-MsolService -Credential $cred`
4. Dans PowerShell, entrez `New-MsolFederatedDomain –SupportMultipleDomain –DomainName`

Utilisez hello suivant les étapes tooadd hello nouveau domaine de niveau supérieur à l’aide d’Azure AD Connect.

1. Lancez Azure AD Connect à partir du bureau de hello ou le menu Démarrer
2. Choisissez « Ajouter un domaine Azure AD supplémentaire » ![Ajouter un domaine Azure AD supplémentaire](./media/active-directory-multiple-domains/add1.png)
3. Entrez votre informations d’identification Azure AD et Active Directory
4. Sélectionnez hello deuxième domaine vous souhaitez tooconfigure pour la fédération.
   ![Ajouter un domaine Azure AD supplémentaire](./media/active-directory-multiple-domains/add2.png)
5. Cliquez sur Installer

### <a name="verify-hello-new-top-level-domain"></a>Vérifiez que le nouveau domaine de niveau supérieur hello
À l’aide de commande PowerShell de hello `Get-MsolDomainFederationSettings -DomainName <your domain>`que vous pouvez afficher hello mis à jour IssuerUri.  capture d’écran Hello ci-dessous montre les paramètres de fédération hello ont été mis à jour sur nos http://bmcontoso.com/adfs/services/trust domaine d’origine

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/MsolDomainFederationSettings.png)

Et toohttps://bmfabrikam.com/adfs/services/trust a été défini à hello IssuerUri sur notre nouveau domaine

![Get-MsolDomainFederationSettings](./media/active-directory-multiple-domains/settings2.png)

## <a name="support-for-sub-domains"></a>Prise en charge des sous-domaines
Lorsque vous ajoutez un sous-domaine, géré de domaines en raison de hello façon Azure AD, elle héritera des paramètres hello du parent de hello.  Cela signifie que hello IssuerUri doit parents de hello toomatch.

Donc, supposons que j’ai bmcontoso.com et que j’ajoute ensuite corp.bmcontoso.com.  Cela signifie que hello IssuerUri pour un utilisateur à partir de corp.bmcontoso.com devez toobe **http://bmcontoso.com/adfs/services/trust.**  Toutefois, les règles standard hello implémentée ci-dessus pour Azure AD, génère un jeton avec un émetteur en tant que **http://corp.bmcontoso.com/adfs/services/trust.** qui ne correspondra pas à la valeur requise du domaine hello et l’authentification échoue.

### <a name="how-tooenable-support-for-sub-domains"></a>Comment tooenable prennent en charge pour les sous-domaines
AD FS de confiance pour Microsoft Online toowork ordre autour de cette hello doit toobe mis à jour.  toodo, vous devez configurer une règle de revendication personnalisée afin qu’il supprime les sous-domaines de suffixe UPN de l’utilisateur hello lors de la construction de valeur d’émetteur hello personnalisé. 

Hello suivant revendication sera procédez comme suit :

    c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

[!NOTE]
dernier numéro de Hello dans l’expression régulière de hello définie hello les domaines parents combien il existe dans votre domaine racine. Dans le cas présent, j’ai bmcontoso.com. Deux domaines parents sont donc nécessaires. Si trois parent domaines ont été toobe conservé (par exemple : corp.bmcontoso.com), puis le nombre de hello aurait été trois. Éventuellement, une plage peut être indiquée, correspondance de hello est toujours effectuée maximum hello toomatch domaines. « {2,3} » correspond à deux domaines toothree (c'est-à-dire : bmfabrikam.com et corp.bmcontoso.com).

Utilisez hello suivant les étapes tooadd un sous-domaines toosupport de revendication personnalisée.

1. Ouvrez Gestion AD FS
2. Cliquez avec le bouton droit sur approbation de partie de confiance en ligne Microsoft hello et choisir les règles de revendication de modifier
3. Sélectionnez la règle de revendication troisième hello et remplacez ![demande de modification](./media/active-directory-multiple-domains/sub1.png)
4. Remplacez la revendication en cours hello :
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)","http://${domain}/adfs/services/trust/"));
   
       with
   
        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"] => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, "^.*@([^.]+\.)*?(?<domain>([^.]+\.?){2})$", "http://${domain}/adfs/services/trust/"));

    ![Remplacer la revendication](./media/active-directory-multiple-domains/sub2.png)

5. Cliquez sur OK.  Cliquez sur Appliquer.  Cliquez sur OK.  Fermez Gestion AD FS.

