---
title: "aaaWhat est inscription libre-service à Azure ? | Microsoft Docs"
description: "Inscription en libre-service une vue d’ensemble pour Azure, comment toomanage hello le processus d’inscription et tootake au-dessus d’un nom de domaine DNS."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: b9f01876-29d1-4ab8-8b74-04d43d532f4b
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: dbf3b59e3807e98f7bf39f3d5591fcde01667323
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-self-service-signup-for-azure"></a>Qu’est-ce qu’une inscription libre-service à Azure ?
Cette rubrique explique le processus d’inscription en libre-service hello et comment tootake au-dessus d’un nom de domaine DNS.  

## <a name="why-use-self-service-signup"></a>Pourquoi utiliser l’inscription libre-service ?
* Get tooservices de clients qu’ils veulent plus rapidement.
* Créer des offres envoyées par e-mail pour un service.
* Créer des flux d’abonnement à un courrier électronique qui autorisent rapidement les identités de toocreate à l’aide de leurs alias de messagerie facile à mémoriser le travail des utilisateurs.
* Les répertoires Azure non gérés peuvent être transformés en répertoires gérés ultérieurement et être réutilisés pour d‘autres services.

## <a name="terms-and-definitions"></a>Termes et définitions
* **Inscription libre-service**: il s’agit hello méthode par laquelle un utilisateur s’inscrit à un service cloud et a une identité automatiquement créée pour eux dans Azure Active Directory (Azure AD) en fonction de leur domaine de messagerie.
* **Annuaire Azure non managé**: il s’agit d’annuaire hello où cette identité est créée. Un répertoire non géré est un répertoire qui ne possède aucun administrateur général.
* **Utilisateur vérifié par e-mail**: type de compte d'utilisateur dans Azure AD. Un utilisateur qui possède une identité créée automatiquement après s’être abonné à une offre libre-service est considéré comme un utilisateur vérifié par e-mail. Un utilisateur vérifié par e-mail est un membre ordinaire d'un répertoire marqué par la valeur creationmethod=EmailVerified.

## <a name="user-experience"></a>Expérience utilisateur
Par exemple, un utilisateur ayant pour adresse e-mail Dan@BellowsCollege.com reçoit les fichiers sensibles par e-mail. fichiers de Hello ont été protégés par Azure Rights Management (Azure RMS). Mais la société de Dan, Bellows College, n’est pas abonnée à Azure RMS, et elle n’a pas déployé Active Directory RMS. Dans ce cas, Dan pouvez souscrire un abonnement gratuit de tooRMS pour les particuliers dans les fichiers de commande tooread hello protégé.

Si Dan est hello premier utilisateur avec une adresse de messagerie à partir de toosign BellowsCollege.com pour cette offre de libre-service, un répertoire non managé sera créé pour BellowsCollege.com dans Azure AD. Si d’autres utilisateurs de domaine de BellowsCollege.com hello s’inscrire pour cette offre ou une offre de libre-service similaire, ils seront également avoir vérifié par courrier électronique des utilisateur des comptes Bonjour non managée du même annuaire dans Azure.

## <a name="admin-experience"></a>Expérience administrateur
Un administrateur qui possède le nom de domaine DNS hello d’un annuaire Azure non managé peut reprendre ou de fusionner le répertoire de hello après prouvez la possession. Hello sections qui suivent expliquent expérience de l’administrateur hello plus en détail, mais voici un résumé :

* Quand vous voulez gérer un annuaire Azure non managé, vous simplement devenez administrateur global de hello du répertoire de non managé hello. On appelle parfois cela une prise en charge interne.
* Lorsque vous fusionnez un annuaire Azure non managé, ajouter de nom de domaine DNS hello du répertoire Azure managé tooyour hello active non managé et un mappage des utilisateurs de ressources est créé par conséquent, les utilisateurs peuvent continuer services tooaccess sans interruption. On appelle parfois cela une prise en charge externe.

## <a name="what-gets-created-in-azure-active-directory"></a>Que permet de créer Azure Active Directory ?
#### <a name="directory"></a>Répertoire
* Un annuaire Azure Active directory pour le domaine de hello est créé, un seul annuaire par domaine.
* Windows Azure AD Hello n’a aucun administrateur général.

#### <a name="users"></a>Utilisateurs
* Pour chaque utilisateur qui s’inscrit, un objet utilisateur est créé dans Windows Azure AD hello.
* Chaque objet utilisateur est considéré comme externe.
* Chaque utilisateur se voit accorder des accès toohello ils souscrit.

### <a name="how-do-i-claim-a-self-service-azure-ad-directory-for-a-domain-i-own"></a>Comment puis-je revendiquer un répertoire Azure AD libre-service pour un domaine qui m’appartient ?
Vous pouvez revendiquer un répertoire Azure AD libre-service en effectuant la validation de domaine. Validation de domaine s’avère domaine de hello propre en créant des enregistrements DNS.

Il existe deux façons toodo une prise en charge DNS d’un annuaire Azure AD :

* prise en charge interne (Admin détecte un annuaire Azure non managé et veut tooturn dans un répertoire)
* reprise externe (Admin tente tooadd un nouveau domaine tootheir Azure répertoire)

Vous serez peut-être intéressé de validation que vous possédez un domaine, car vous tirez sur un répertoire non managé après un utilisateur a effectué l’inscription en libre-service, ou ajouter un nouveau domaine tooan existant géré répertoire. Par exemple, vous avez un domaine nommé contoso.com et que vous voulez tooadd un nouveau domaine nommé contoso.co.uk ou contoso.uk.

## <a name="what-is-domain-takeover"></a>Qu’est-ce que la prise en charge d’un domaine ?
Cette section décrit comment toovalidate que vous possédez un domaine

### <a name="what-is-domain-validation-and-why-is-it-used"></a>Qu’est-ce que la validation de domaine et pourquoi est-elle utilisée ?
Dans les opérations de tooperform de commande sur un répertoire, Azure AD nécessite que vous validez le propriétaire du domaine DNS de hello.  La validation du domaine de hello permet de répertoire hello tooclaim et soit promouvoir hello libre-service tooa managé répertoire ou répertoire de libre-service de hello de fusion en un existant géré active.

## <a name="examples-of-domain-validation"></a>Exemples de validation de domaine
Il existe deux façons toodo une prise en charge DNS d’un répertoire :

* prise en charge interne (par exemple, un administrateur détecte un annuaire en libre-service, non managé et souhaite tooturn dans le répertoire géré)
* prise en charge externe (par exemple, un administrateur tente tooadd un nouveau domaine tooa répertoire)

### <a name="internal-takeover---promote-a-self-service-unmanaged-directory-toobe-a-managed-directory"></a>Prise en charge interne - promouvoir un toobe en libre-service, non managé active un répertoire
Lorsque vous effectuez la prise en charge interne, active de hello convertir à partir d’un répertoire managé tooa de répertoire non managé. Vous devez la validation du nom du domaine DNS toocomplete, où vous créez un enregistrement MX ou un enregistrement TXT dans la zone DNS de hello. Cette action :

* Valide que vous possédez hello domaine
* Rend le répertoire hello géré
* Rend vous hello administrateur général du répertoire de hello

Supposons qu’un administrateur à partir de l’Université de soufflets détecte que les utilisateurs à l’école de hello êtes inscrit pour les offres de libre-service. Hello enregistré propriétaire de hello DNS nom BellowsCollege.com, hello administrateur informatique peut valider la propriété de nom DNS de hello dans Azure et d’agir sur le répertoire de non managé hello. Hello active devient alors un répertoire, et hello administrateur rôle hello administrateur global pour le répertoire de BellowsCollege.com hello.

### <a name="external-takeover---merge-a-self-service-directory-into-an-existing-managed-directory"></a>Prise en charge externe : fusionner un répertoire libre-service avec un répertoire géré existant
Dans une prise en charge externe, vous disposez déjà d’un répertoire et vous voulez tous les utilisateurs et groupes à partir d’un toojoin active non managé qui gérés active, plutôt que deux propre des répertoires distincts.

En tant qu’administrateur d’un répertoire, vous ajoutez un domaine, et ce domaine produit toohave un répertoire non managé associé.

Par exemple, supposons que vous êtes un administrateur informatique et que vous disposez déjà d’un répertoire pour Contoso.com, un nom de domaine qui est inscrit tooyour organisation. Vous découvrez que des utilisateurs de votre société se sont inscrits en libre-service à une offre en utilisant un nom de domaine de messagerie user@contoso.co.uk, qui est un autre nom de domaine appartenant à votre entreprise. Ces utilisateurs possèdent actuellement des comptes dans un répertoire non géré pour contoso.co.uk.

Vous ne souhaitez pas toomanage deux répertoires distinct, afin de vous fusionnez répertoire non managé hello contoso.co.uk dans votre annuaire gérés existant pour contoso.com.

Suit prise de contrôle externe hello même processus de validation de DNS en tant que la prise en charge interne.  Différence étant : les utilisateurs et les services sont remappé toohello informatique répertoire géré.

#### <a name="whats-hello-impact-of-performing-an-external-takeover"></a>Nouveautés d’impact hello d’effectuer une reprise externe ?
Avec une prise en charge externe, un mappage des utilisateurs de ressources est créé pour les utilisateurs peuvent continuer de services tooaccess sans interruption. De nombreuses applications, y compris de RMS pour les particuliers, gèrent également les mappage hello des utilisateurs aux ressources, et les utilisateurs peuvent continuer à tooaccess ces services sans modification. Si une application ne gère pas efficacement le mappage hello des utilisateurs aux ressources, prise en charge externe peut être explicitement bloqué tooprevent des utilisateurs à partir d’une mauvaise expérience.

#### <a name="directory-takeover-support-by-service"></a>Prise en charge du répertoire par le service
Actuellement prise en charge de la prise en charge des services de hello suivant :

* RMS

Hello suivant services sera bientôt prenant en charge prise en charge :

* PowerBI

suivante de Hello ne le faites pas et nécessite des données d’utilisateur admin supplémentaires action toomigrate après une prise en charge externe.

* SharePoint/OneDrive

## <a name="how-tooperform-a-dns-domain-name-takeover"></a>Prise en charge de noms tooperform un domaine DNS
Vous avez plusieurs options pour le tooperform une validation de domaine (et une prise en charge si vous le souhaitez) :

1. Portail de gestion Azure

   Une prise en charge est déclenchée lors de l’ajout d’un domaine.  Si un répertoire existe déjà pour le domaine de hello, vous devrez hello option tooperform une prise en charge externe.

   Se connecter toohello portail Azure à l’aide de vos informations d’identification.  Accédez tooyour un annuaire existant, puis trop**ajouter un domaine**.
2. Office 365

   Vous pouvez utiliser les options hello hello [gérer les domaines](https://support.office.com/article/Navigate-to-the-Office-365-Manage-domains-page-026af1f2-0e6d-4f2d-9b33-fd147420fac2/) page toowork Office 365 avec vos domaines et les enregistrements DNS. Consultez [Vérifier votre domaine dans Office 365](https://support.office.com/article/Verify-your-domain-in-Office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611/).
3. Windows PowerShell

   Hello suit est requis tooperform une validation à l’aide de Windows PowerShell.

   | Étape | Applet de commande toouse |
   | --- | --- |
   | Créer un objet d'informations d'identification |Get-Credential |
   | Se connecter tooAzure AD |Connect-MsolService |
   | obtenir une liste de domaines |Get-MsolDomain |
   | Créer un test |Get-MsolDomainVerificationDns |
   | Créer un enregistrement DNS |Effectuer cette opération sur votre serveur DNS |
   | Vérifier hello test |Confirm-MsolEmailVerifiedDomain |

Par exemple :

1. Se connecter tooAzure AD utilisant les informations d’identification de hello ont été utilisés toorespond toohello libre-service offre :

        import-module MSOnline
        $msolcred = get-credential
        connect-msolservice -credential $msolcred
2. Obtenez une liste de domaines :

    Get-MsolDomain
3. Ensuite, exécutez toocreate d’applet de commande Get-MsolDomainVerificationDns hello une stimulation :

    Get-MsolDomainVerificationDns –DomainName *votre_nom_de_domaine* –Mode DnsTxtRecord

    Par exemple :

    Get-MsolDomainVerificationDns –DomainName contoso.com – Mode DnsTxtRecord
4. Copiez la valeur hello (stimulation hello) est retournée à partir de cette commande.

    Par exemple :

    MS=32DD01B82C05D27151EA9AE93C5890787F0E65D9
5. Dans votre espace de noms DNS public, créez un enregistrement txt DNS qui contient la valeur hello que vous avez copiée à l’étape précédente de hello.

    nom Hello de cet enregistrement est hello du nom de domaine parent de hello, par conséquent, si vous créez cet enregistrement de ressource à l’aide du rôle DNS de hello à partir de Windows Server, hello enregistrement nom vide et copiez hello valeur dans la zone de texte hello
6. Le défi hello tooverify hello Confirm-MsolDomain applet de commande, exécutez :

    Confirm-MsolEmailVerifiedDomain -DomainName *votre_nom_de_domaine*

    Par exemple :

    Confirm-MsolEmailVerifiedDomain -DomainName contoso.com

Un test réussi vous renvoie invite toohello sans erreur.

## <a name="how-do-i-control-self-service-settings"></a>Comment vérifier les paramètres libre-service ?
Les administrateurs peuvent désormais effectuer deux vérifications libre-service. Ils peuvent vérifier :

* Indique si les utilisateurs peuvent joindre l’annuaire de hello par courrier électronique.
* Si les utilisateurs peuvent s’abonner eux-mêmes aux applications et services.

### <a name="how-can-i-control-these-capabilities"></a>Comment puis-je vérifier ces fonctionnalités ?
Un administrateur peut configurer ces fonctionnalités à l'aide des paramètres Set-MsolCompanySettings de cet applet de commande Azure AD :

* **AllowEmailVerifiedUsers** vérifie si un utilisateur peut créer ou rejoindre un répertoire non géré. Si vous définissez ce paramètre trop$ false, n’est vérifiée par courrier électronique les utilisateurs peuvent joindre l’annuaire de hello.
* **AllowAdHocSubscriptions** contrôle la possibilité de hello pour les utilisateurs libre-service de tooperform s’inscrire. Si vous définissez ce paramètre trop$ false, aucun utilisateur ne peut effectuer inscription en libre-service.

### <a name="how-do-hello-controls-work-together"></a>Comment les contrôles hello fonctionnent ensemble ?
Ces deux paramètres peuvent être utilisés en conjonction toodefine s’inscrire un contrôle plus précis sur le libre-service. Par exemple, hello commande suivante autorise les utilisateurs tooperform inscription libre service, mais uniquement si ces utilisateurs ont déjà un compte dans Azure AD (en d’autres termes, les utilisateurs qui doivent une toobe est vérifiée par courrier électronique un compte créé ne peut pas effectuer inscription en libre-service) :

    Set-MsolCompanySettings -AllowEmailVerifiedUsers $false -AllowAdHocSubscriptions $true

Hello organigramme suivant décrit tous les hello différentes combinaisons de ces paramètres et hello résultant conditions liées au répertoire de hello et d’inscription libre-service.

![][1]

Pour plus d’informations et des exemples de toouse ces paramètres, voir [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0).

## <a name="see-also"></a>Voir aussi
* [Comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview)
* [Azure PowerShell](/powershell/azure/overview)
* [Guide de référence des applets de commande Azure](/powershell/azure/get-started-azureps)
* [Set-MsolCompanySettings](/powershell/module/msonline/set-msolcompanysettings?view=azureadps-1.0)

<!--Image references-->
[1]: ./media/active-directory-self-service-signup/SelfServiceSignUpControls.png
