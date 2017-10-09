---
title: "Azure AD Connect : topologies prises en charge | Microsoft Docs"
description: "Cette rubrique détaille les topologies prises en charge et celles qui ne le sont pas pour Azure AD Connect"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 1034c000-59f2-4fc8-8137-2416fa5e4bfe
ms.service: active-directory
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: identity
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 41632a54e8e85492fbf1a751ef4e618c8870abe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="topologies-for-azure-ad-connect"></a>Topologies pour Azure AD Connect
Cet article décrit les différentes topologies d’Azure Active Directory (Azure AD) qui utilisent la synchronisation Azure AD Connect comme solution d’intégration clés hello et locaux. Cet article inclut les configurations prises en charge et celles qui ne le sont pas.

Voici une légende hello pour les images dans l’article de hello :

| Description | Symbole |
| --- | --- |
| Forêt Active Directory locale |![Forêt Active Directory locale](./media/active-directory-aadconnect-topologies/LegendAD1.png) |
| Active Directory local avec importation filtrée |![Active Directory avec importation filtrée](./media/active-directory-aadconnect-topologies/LegendAD2.png) |
| Serveur Azure AD Connect Sync |![Serveur Azure AD Connect Sync](./media/active-directory-aadconnect-topologies/LegendSync1.png) |
| « Mode intermédiaire » du serveur Azure AD Connect Sync |![« Mode intermédiaire » du serveur Azure AD Connect Sync](./media/active-directory-aadconnect-topologies/LegendSync2.png) |
| GALSync avec Forefront Identity Manager (FIM) 2010 ou Microsoft Identity Manager (MIM) 2016 |![GALSync avec FIM 2010 ou MIM 2016](./media/active-directory-aadconnect-topologies/LegendSync3.png) |
| Serveur Azure AD Connect Sync, détaillé |![Serveur Azure AD Connect Sync, détaillé](./media/active-directory-aadconnect-topologies/LegendSync4.png) |
| Azure AD |![Azure Active Directory](./media/active-directory-aadconnect-topologies/LegendAAD.png) |
| Scénario non pris en charge |![Scénario non pris en charge](./media/active-directory-aadconnect-topologies/LegendUnsupported.png) |

## <a name="single-forest-single-azure-ad-tenant"></a>Une seule forêt, un seul client Azure AD
![Topologie pour une forêt unique et un locataire unique](./media/active-directory-aadconnect-topologies/SingleForestSingleDirectory.png)

Hello plus topologie la plus fréquente est une seule sur le site de la forêt, avec l’un ou plusieurs domaines et une annonce Azure locataire. L’authentification Azure AD est effectuée avec la synchronisation de mot de passe. installation rapide de Hello d’Azure AD Connect prend en charge uniquement dans cette topologie.

### <a name="single-forest-multiple-sync-servers-tooone-azure-ad-tenant"></a>Forêt unique, plusieurs locataire de tooone Azure AD de serveurs de synchronisation
![Topologie filtrée pour une forêt unique non prise en charge](./media/active-directory-aadconnect-topologies/SingleForestFilteredUnsupported.png)

Avoir plusieurs serveurs de synchronisation Azure AD Connect toohello connecté même instance Azure AD client n’est pas pris en charge, sauf pour une [serveur intermédiaire](#staging-server). Il a non pris en charge même si ces serveurs sont toosynchronize configuré avec un ensemble mutuellement exclusif d’objets. Vous pouvez considéré cette topologie si vous ne pouvez atteindre tous les domaines de la forêt hello à partir d’un serveur unique, ou si vous souhaitez toodistribute charge entre plusieurs serveurs.

## <a name="multiple-forests-single-azure-ad-tenant"></a>Plusieurs forêts, un seul client Azure AD
![Topologie pour plusieurs forêts et un locataire unique](./media/active-directory-aadconnect-topologies/MultiForestSingleDirectory.png)

De nombreuses organisations possèdent des environnements comportant plusieurs forêts Active Directory locales. Il existe plusieurs raisons de déployer plus d’une forêt Active Directory locale. Conceptions avec compte-ressource forêts et hello le résultat d’une fusion ou une acquisition sont des exemples classiques.

Lorsque vous avez plusieurs forêts, toutes les forêts doivent être accessibles par un même serveur Azure AD Connect Sync. Vous n’avez domaine de tooa server toojoin hello. Si nécessaire tooreach toutes les forêts, vous pouvez placer hello serveur dans un réseau de périmètre (également appelé DMZ, zone démilitarisée et sous-réseau filtré).

Assistant d’installation Bonjour Azure AD Connect propose plusieurs options tooconsolidate qui sont représentés dans plusieurs forêts. objectif de Hello est qu’un utilisateur est représenté une seule fois dans Azure AD. Il existe certaines topologies courantes que vous pouvez configurer dans chemin d’installation personnalisée hello dans l’Assistant installation hello. Sur hello **identifiant de manière unique les utilisateurs** option hello sélectionnez correspondante qui représente la topologie de votre page. consolidation de Hello est configurée uniquement pour les utilisateurs. Les groupes en double ne sont pas consolidées hello configuration par défaut.

Les topologies courantes sont décrites dans les sections hello sur [topologies séparées](#multiple-forests-separate-topologies), [maillée](#multiple-forests-full-mesh-with-optional-galsync), et [hello topologie compte-ressource](#multiple-forests-account-resource-forest).

configuration par défaut de Hello dans la synchronisation Azure AD Connect suppose que :

* Chaque utilisateur possède un seul compte activé, et la forêt hello où se trouve ce compte est utilisé tooauthenticate hello. Cette supposition comprend la synchronisation des mots de passe et la fédération. UserPrincipalName et sourceAnchor/immutableID proviennent de cette forêt.
* Chaque utilisateur n’a qu’une seule boîte aux lettres.
* forêt Hello qui héberge les boîtes aux lettres hello pour un utilisateur a la meilleure qualité de données hello pour les attributs visibles dans la liste d’adresses globale (LAG) Exchange de hello. S’il n’existe aucune boîte aux lettres pour l’utilisateur de hello, n’importe quelle forêt peut être toocontribute utilisé ces valeurs d’attribut.
* Si vous avez une boîte aux lettres liée, il existe également un compte dans une forêt différente de celle utilisée pour la connexion.

Si votre environnement ne correspond pas à ces hypothèses, hello événements suivants se produisent :

* Si vous avez plusieurs comptes actifs ou plusieurs boîtes aux lettres, moteur de synchronisation hello choisit un et ignore hello autres.
* Une boîte aux lettres liée avec aucun autre compte actif n’est pas exporté tooAzure AD. compte d’utilisateur Hello n’est pas représentée en tant que membre d’un groupe. Dans DirSync, une boîte aux lettres liée est toujours représentée comme une boîte aux lettres normale. Cette modification est intentionnellement un scénario de forêts multiples de prise en charge toobetter un comportement différent.

Vous trouverez plus de détails dans [présentation de la configuration par défaut hello](active-directory-aadconnectsync-understanding-default-configuration.md).

### <a name="multiple-forests-multiple-sync-servers-tooone-azure-ad-tenant"></a>Plusieurs forêts, plusieurs locataires de tooone Azure AD de serveurs de synchronisation
![Topologie non prise en charge pour plusieurs forêts et plusieurs serveurs de synchronisation](./media/active-directory-aadconnect-topologies/MultiForestMultiSyncUnsupported.png)

Avoir plusieurs tooa de serveur connecté de synchronisation Azure AD Connect unique du locataire Azure AD n’est pas pris en charge. exception Hello est utiliser hello un [serveur intermédiaire](#staging-server).

### <a name="multiple-forests-separate-topologies"></a>Plusieurs forêts, topologies distinctes
![Option pour ne représenter les utilisateurs qu’une seule fois à travers tous les annuaires](./media/active-directory-aadconnect-topologies/MultiForestUsersOnce.png)

![Représentation de plusieurs forêts et de topologies distinctes](./media/active-directory-aadconnect-topologies/MultiForestSeperateTopologies.png)

Dans cet environnement, toutes les forêts locales sont traitées comme des entités distinctes. Aucun utilisateur n’est présent dans une autre forêt. Chaque forêt possède sa propre organisation Exchange, et il n’existe aucune opération GALSync entre les forêts hello. Cette topologie peut être situation hello après une fusion-acquisition ou dans une organisation où chaque unité commerciale fonctionne de manière indépendante. Ces forêts sont dans hello même organisation dans Azure AD et s’affichent avec une liste d’adresses globale unifiée. Bonjour précédant l’image, chaque objet dans chaque forêt est représenté une seule fois dans le métaverse de hello et agrégée dans le locataire d’Azure AD cible hello.

### <a name="multiple-forests-match-users"></a>Plusieurs forêts : utilisateurs en correspondance
Common tooall ces scénarios est cette distribution et groupes de sécurité peuvent contenir des utilisateurs, des contacts et des principaux de sécurité (FSP). FSP est utilisés dans les membres de toorepresent de Services de domaine Active Directory (AD DS) à partir d’autres forêts dans un groupe de sécurité. Tous les FSP est objet réel de toohello résolu dans Azure AD.

### <a name="multiple-forests-full-mesh-with-optional-galsync"></a>Plusieurs forêts : maillage complet avec GALSync facultative
![Option d’utilisation de l’attribut de messagerie hello pour la correspondance lorsque les identités utilisateurs existent sur plusieurs annuaires](./media/active-directory-aadconnect-topologies/MultiForestUsersMail.png)

![Topologie de maillage complet pour plusieurs forêts](./media/active-directory-aadconnect-topologies/MultiForestFullMesh.png)

Une topologie de maille pleine permet aux utilisateurs et toobe ressources situé dans n’importe quelle forêt. En règle générale, il existe des approbations bidirectionnelles entre les forêts hello.

Si Exchange est présent dans plusieurs forêts, il peut (éventuellement) y avoir une solution GALSync locale. Chaque utilisateur est ensuite représenté en tant que contact dans toutes les autres forêts. GALSync est fréquemment implémentée via FIM 2010 ou MIM 2016. Azure AD Connect ne peut pas être utilisé pour une GALSync locale.

Dans ce scénario, les objets d’identité sont jointes via l’attribut de messagerie hello. Un utilisateur qui dispose d’une boîte aux lettres dans une forêt est joint avec des contacts hello Bonjour autres forêts.

### <a name="multiple-forests-account-resource-forest"></a>Plusieurs forêts : forêt de ressources de comptes
![Option d’utilisation d’attributs ObjectSID et msExchMasterAccountSID de hello correspondant lorsqu’il existent des identités sur plusieurs annuaires](./media/active-directory-aadconnect-topologies/MultiForestUsersObjectSID.png)

![Topologie de forêt de ressources de comptes pour plusieurs forêts](./media/active-directory-aadconnect-topologies/MultiForestAccountResource.png)

Dans une topologie de forêt de ressources de comptes, vous avez une ou plusieurs forêts de *comptes* avec des comptes d’utilisateurs actifs. Une ou plusieurs forêts de *ressources* comportent également des comptes désactivés.

Dans ce scénario, une (ou plusieurs) forêt de ressources approuve toutes les forêts de comptes. forêt de ressources Hello a généralement un schéma Active Directory étendu avec Exchange et Lync. Tous les services Exchange et Lync, et d’autres services partagés, sont situés dans cette forêt. Les utilisateurs ont un compte d’utilisateur désactivé dans cette forêt, et les boîtes aux lettres hello est lié forêt de comptes toohello.

## <a name="office-365-and-topology-considerations"></a>Considérations sur Office 365 et la topologie
Certaines charges de travail Office 365 ont certaines restrictions quant aux topologies prises en charge :

| Charge de travail | Restrictions |
--------- | ---------
| Exchange Online | S’il existe plus d’une organisation d’Exchange sur site (autrement dit, Exchange a été déployé toomore qu’une seule forêt), vous devez utiliser Exchange 2013 SP1 ou version ultérieure. Pour plus d’informations, consultez la rubrique [Déploiements hybrides à forêts Active Directory multiples](https://technet.microsoft.com/library/jj873754.aspx). |
| Skype Entreprise | Lorsque vous utilisez plusieurs forêts locales, la seule topologie de forêt compte-ressource hello est pris en charge. Pour plus d’informations, consultez la rubrique [Configuration environnementale pour Skype for Business Server 2015](https://technet.microsoft.com/library/dn933910.aspx). |


## <a name="staging-server"></a>Serveur de test
![Serveur intermédiaire dans une topologie](./media/active-directory-aadconnect-topologies/MultiForestStaging.png)

Azure AD Connect prend en charge l’installation d’un second serveur en *mode intermédiaire*. Un serveur dans ce mode lit les données à partir de tous les annuaires connectés, mais n’écrit pas les répertoires tooconnected. Il utilise le cycle de synchronisation normale hello et donc une copie mise à jour des données d’identité hello.

Dans un incident où le serveur principal de hello échoue, vous pouvez basculer toohello serveur intermédiaire. Pour cela, dans l’Assistant d’Azure AD Connect hello. Ce deuxième serveur peut se trouver dans un autre centre de données, car aucune infrastructure n’est partagé avec le serveur principal de hello. Vous devez copier manuellement les modifications de configuration apportées sur le second serveur hello serveur principal toohello.

Vous pouvez utiliser un tootest serveur intermédiaire un effet personnalisé nouvelle configuration et hello sur vos données. Vous pouvez afficher un aperçu des modifications de hello et ajustez les paramètres de hello. Lorsque vous êtes satisfait de la nouvelle configuration de hello, vous pouvez rendre hello intermédiaire active serveur hello et définir des hello ancien active toostaging mode serveur.

Vous pouvez également utiliser ce serveur de synchronisation Directory méthode tooreplace hello. Préparer le nouveau serveur de hello et définir le mode toostaging. Assurez-vous qu’il est en bon état, les désactiver (ce qui active), le mode de mise en lots et arrêter le serveur actif de hello.

Il est possible toohave plus que d’un serveur intermédiaire lorsque vous souhaitez toohave plusieurs sauvegardes dans différents centres de données.

## <a name="multiple-azure-ad-tenants"></a>Plusieurs clients Azure AD
Nous recommandons d’avoir un seul locataire dans Azure AD pour une organisation.
Avant de planifier toouse plusieurs locataires Azure AD, consultez l’article de hello [gestion des unités administratives dans Azure AD](../active-directory-administrative-units-management.md). Il couvre les scénarios courants dans lesquels vous pouvez utiliser un locataire unique.

![Topologie pour plusieurs forêts et plusieurs locataires](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectory.png)

Il existe une relation 1:1 entre un serveur Azure AD Connect Sync et un locataire Azure AD. Pour chaque client Azure AD, vous avez besoin d’une installation d’un serveur de synchronisation Azure AD Connect. instances de locataire Azure AD Hello sont isolés par conception. Autrement dit, les utilisateurs dans un locataire ne peut pas voir utilisateurs Bonjour autre client. Si vous souhaitez cette séparation, cette configuration est prise en charge. Dans le cas contraire, vous devez utiliser hello unique de modèle de client Azure AD.

### <a name="each-object-only-once-in-an-azure-ad-tenant"></a>Chaque objet une seule fois dans un client Azure AD
![Topologie filtrée pour une forêt unique](./media/active-directory-aadconnect-topologies/SingleForestFiltered.png)

Dans cette topologie, un serveur de synchronisation Azure AD Connect est tooeach connecté Azure AD client. serveurs de synchronisation Azure AD Connect Hello doivent être configurés pour le filtrage afin que chacune possède un ensemble d’objets toooperate mutuellement. Vous pouvez, par exemple, limiter chaque domaine particulier tooa de serveur ou l’unité d’organisation.

Un domaine DNS peut être inscrit dans un seul locataire Azure AD. Hello UPN des utilisateurs hello dans l’instance d’Active Directory local hello doit également utiliser des espaces de noms distincts. Par exemple, Bonjour précédant l’image, trois suffixes UPN distincts sont enregistrés dans l’instance d’Active Directory local hello : wingtiptoys.com contoso.com et fabrikam.com. les utilisateurs de Hello dans chaque domaine d’Active Directory local utiliser un espace de noms différents.

Il n’y a aucune opération GALSync entre instances de locataire Azure AD hello. Bonjour carnet d’adresses dans Exchange Online et Skype pour indique d’entreprise uniquement les utilisateurs de hello même client.

Cette topologie comporte suivants de hello restrictions sur sinon les scénarios pris en charge :

* Seul l’un des clients de hello Azure AD peut activer un hybride d’Exchange avec une instance d’Active Directory local hello.
* Les appareils Windows 10 ne peuvent être associés qu’à un seul locataire Azure AD.
* Hello unique (SSO de) l’option de connexion pour l’authentification directe et de synchronisation de mot de passe peut être utilisée avec un seul locataire Azure AD.

Hello pour un ensemble mutuellement exclusif d’objets s’applique également toowriteback. Certaines fonctionnalités d’écriture différée ne sont pas prises en charge avec cette topologie, car elles supposent une seule configuration locale. Voici quelques fonctionnalités :

* Écriture différée des groupes avec la configuration par défaut.
* Écriture différée des appareils.

### <a name="each-object-multiple-times-in-an-azure-ad-tenant"></a>Chaque objet plusieurs fois dans un client Azure AD
![Topologie non prise en charge pour une forêt unique et plusieurs locataires](./media/active-directory-aadconnect-topologies/SingleForestMultiDirectoryUnsupported.png) ![Topologie non prise en charge pour une forêt unique et plusieurs connecteurs](./media/active-directory-aadconnect-topologies/SingleForestMultiConnectorsUnsupported.png)

Les tâches suivantes ne sont pas prises en charge :

* Synchronisation hello identiques aux clients d’utilisateur toomultiple Azure AD.
* Modification d’une configuration pour faire en sorte que les utilisateurs dans un locataire Azure AD apparaissent comme contacts dans un autre locataire Azure AD.
* Modifier les clients Azure AD Connect synchronisation tooconnect toomultiple Azure AD.

### <a name="galsync-by-using-writeback"></a>GALSync à l’aide de l’écriture différée
![Topologie non prise en charge pour plusieurs forêts et plusieurs annuaires, avec GALSync se concentrant sur Azure AD](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync1Unsupported.png) ![Topologie non prise en charge pour plusieurs forêts et plusieurs annuaires, avec GALSync se concentrant sur Active Directory local](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync2Unsupported.png)

Les locataires Azure AD sont isolés de par leur conception. Les tâches suivantes ne sont pas prises en charge :

* Modifier la configuration hello Azure AD Connect tooread de données de synchronisation à partir d’une autre locataire Azure AD.
* Exporter des utilisateurs en tant qu’instance de contacts tooanother locale Active Directory à l’aide de synchronisation Azure AD Connect.

### <a name="galsync-with-on-premises-sync-server"></a>GALSync avec le serveur de synchronisation local
![GALSync dans une topologie pour plusieurs forêts et plusieurs annuaires](./media/active-directory-aadconnect-topologies/MultiForestMultiDirectoryGALSync.png)

Vous pouvez utiliser FIM 2010 ou MIM 2016 toosync les utilisateurs locaux (via GALSync) entre deux organisations Exchange. les utilisateurs de Hello dans une organisation apparaissent en tant qu’utilisateurs/contacts à l’étranger dans hello autre organisation. Ces différentes instances Active Directory locales peuvent ensuite être synchronisées vers leurs propres locataires Azure AD.

## <a name="next-steps"></a>Étapes suivantes
toolearn tooinstall Azure AD Connect pour ces scénarios, voir [installation personnalisée d’Azure AD Connect](active-directory-aadconnect-get-started-custom.md).

En savoir plus sur hello [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuration.

En savoir plus sur [l’intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).
