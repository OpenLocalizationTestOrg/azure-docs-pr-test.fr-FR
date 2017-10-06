---
title: aaaGeneric connecteur LDAP | Documents Microsoft
description: "Cet article décrit comment le connecteur LDAP générique de tooconfigure Microsoft."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 984beeb0-4d91-4908-ad81-c19797c4891b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 25031b4da196bd073902b04b0705762bfa0118b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-ldap-connector-technical-reference"></a>Référence technique au connecteur LDAP générique
Cet article décrit hello connecteur LDAP générique. article de Hello s’applique toohello suite de produits :

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Nécessité d’utiliser le correctif logiciel 4.1.3671.0 ou une version ultérieure [KB3092178](https://support.microsoft.com/kb/3092178).

MIM2016 et FIM2010R2, hello Connector est disponible en téléchargement à partir de hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

Lorsque vous faites référence tooIETF RFC, ce document utilise un format hello (RFC [RFC number] / [section dans le document RFC]), par exemple (RFC 4512/4.3).
Vous trouverez plus d’informations à http://tools.ietf.org/html/rfc4500 (vous devez tooreplace 4500 avec le nombre RFC correct hello).

## <a name="overview-of-hello-generic-ldap-connector"></a>Vue d’ensemble de hello connecteur LDAP générique
Hello connecteur LDAP générique permet de vous toointegrate hello service de synchronisation avec un serveur LDAP v3.

Certaines opérations et les éléments de schéma, telles que celles nécessaires Importation delta de tooperform, ne sont pas spécifiés dans la RFC de l’IETF hello. Pour ces opérations, seuls les annuaires LDAP spécifiés explicitement sont pris en charge.

À partir d’un point de vue global, hello suivant les fonctionnalités est prises en charge par la version actuelle de hello du connecteur de hello :

| Fonctionnalité | Support |
| --- | --- |
| Source de données connectée |Connecteur de Hello est pris en charge avec tous les serveurs de v3 LDAP (RFC 4510 conforme). Il a été testé avec les éléments suivants de hello : <li>Microsoft Active Directory Lightweight Directory Services (AD LDS)</li><li>Catalogue global Microsoft Active Directory (AD GC)</li><li>Serveur d’annuaire 389</li><li>Apache Directory Server</li><li>IBM Tivoli DS</li><li>Isode Directory</li><li>NetIQ eDirectory</li><li>Novell eDirectory</li><li>Open DJ</li><li>Open DS</li><li>Open LDAP (openldap.org)</li><li>Oracle (précédemment Sun) Directory Server Enterprise Edition</li><li>RadiantOne Virtual Directory Server (VDS)</li><li>Sun One Directory Server</li>**Répertoires notables non pris en charge :** <li>Microsoft Active Directory domaine Services (AD DS) [Utilisez hello intégrés connecteur Active Directory à la place]</li><li>Oracle Internet Directory (OID)</li> |
| Scénarios |<li>Gestion du cycle de vie des objets</li><li>Gestion des groupes</li><li>Gestion des mots de passe</li> |
| Opérations |Hello opérations suivantes est prises en charge sur tous les annuaires LDAP : <li>Importation complète</li><li>Exportation</li>Hello opérations suivantes est uniquement pris en charge sur les répertoires spécifiés :<li>Importation différentielle</li><li>Définition du mot de passe, modification du mot de passe</li> |
| Schéma |<li>Schéma est détecté à partir du schéma LDAP hello (RFC3673 et RFC4512/4.2)</li><li>Prend en charge des classes structurelles, les classes auxiliaires et la classe d’objets extensibleObject (RFC4512/4.3)</li> |

### <a name="delta-import-and-password-management-support"></a>Importation différentielle et prise en charge de la gestion par mot de passe
Les répertoires pris en charge pour l’importation différentielle et la gestion de mot de passe :

* Microsoft Active Directory Lightweight Directory Services (AD LDS)
  * Prend en charge toutes les opérations d’importation différentielle
  * Prend en charge la définition de mot de passe
* Catalogue global Microsoft Active Directory (AD GC)
  * Prend en charge toutes les opérations d’importation différentielle
  * Prend en charge la définition de mot de passe
* Serveur d’annuaire 389
  * Prend en charge toutes les opérations d’importation différentielle
  * Prend en charge la définition de mot de passe et la modification de mot de passe
* Apache Directory Server
  * Ne prend pas en charge l’importation différentielle depuis ce répertoire n’a pas de journal des modifications persistantes
  * Prend en charge la définition de mot de passe
* IBM Tivoli DS
  * Prend en charge toutes les opérations d’importation différentielle
  * Prend en charge la définition de mot de passe et la modification de mot de passe
* Isode Directory
  * Prend en charge toutes les opérations d’importation différentielle
  * Prend en charge la définition de mot de passe et la modification de mot de passe
* Novell eDirectory et NetIQ eDirectory
  * Prend en charge les opérations d’ajout, de mise à jour et de renommage pour l’importation différentielle
  * Ne prend pas en charge les opérations de suppression pour l’importation différentielle
  * Prend en charge la définition de mot de passe et la modification de mot de passe
* Open DJ
  * Prend en charge toutes les opérations d’importation différentielle
  * Prend en charge la définition de mot de passe et la modification de mot de passe
* Open DS
  * Prend en charge toutes les opérations d’importation différentielle
  * Prend en charge la définition de mot de passe et la modification de mot de passe
* Open LDAP (openldap.org)
  * Prend en charge toutes les opérations d’importation différentielle
  * Prend en charge la définition de mot de passe
  * Ne prend pas en charge la modification de mot de passe
* Oracle (précédemment Sun) Directory Server Enterprise Edition
  * Prend en charge toutes les opérations d’importation différentielle
  * Prend en charge la définition de mot de passe et la modification de mot de passe
* RadiantOne Virtual Directory Server (VDS)
  * Doit utiliser la version 7.1.1 ou une version ultérieure
  * Prend en charge toutes les opérations d’importation différentielle
  * Prend en charge la définition de mot de passe et la modification de mot de passe
* Sun One Directory Server
  * Prend en charge toutes les opérations d’importation différentielle
  * Prend en charge la définition de mot de passe et la modification de mot de passe

### <a name="prerequisites"></a>Composants requis
Avant d’utiliser hello connecteur, vérifiez que vous disposer de hello sur le serveur de synchronisation hello :

* Microsoft .NET 4.5.2 Framework ou version ultérieure

### <a name="detecting-hello-ldap-server"></a>Détection de serveur LDAP de hello
Hello connecteur s’appuie sur les différentes techniques toodetect et identifier le serveur LDAP de hello. Hello connecteur utilise hello DSE racine, nom/version du fournisseur, et elle inspecte les objets de hello schéma toofind uniques et les attributs connus tooexist dans certains serveurs LDAP. Ces données, si trouvée, est utilisé toopre-remplir des options de configuration hello Bonjour connecteur.

### <a name="connected-data-source-permissions"></a>Autorisations de la source de données connectée
tooperform importer et exporter des opérations sur les objets dans l’annuaire connecté de hello hello, le compte de connecteur de hello doit disposer des autorisations suffisantes. connecteur de Hello doit écrire tooexport en mesure d’autorisations toobe et tooimport en mesure de toobe autorisations de lecture. Configuration de l’autorisation est effectuée dans les expériences de gestion hello du répertoire cible de hello lui-même.

### <a name="ports-and-protocols"></a>Ports et protocoles
connecteur de Hello utilise le numéro de port de hello spécifiée dans la configuration de hello, qui par défaut est 389 pour LDAP et 636 pour le protocole LDAPS.

Pour le protocole LDAPS, vous devez utiliser SSL 3.0 ou TLS. SSL 2.0 n’est pas pris en charge et ne peut être activé.

### <a name="required-controls-and-features"></a>Fonctionnalités et contrôles requis
Hello contrôles/fonctionnalités LDAP suivants doivent être disponibles sur le serveur LDAP de hello pour hello connecteur toowork correctement :  
`1.3.6.1.4.1.4203.1.5.3` Filtres True/False

filtre de la valeur True/False Hello n’est souvent pas signalée comme pris en charge par les annuaires LDAP et peut apparaître dans hello **Page Global** sous **fonctionnalités obligatoire introuvable**. Il est utilisé toocreate **ou** filtres dans les requêtes LDAP, par exemple lors de l’importation de plusieurs types d’objets. Si vous pouvez importer plusieurs types d’objets, votre serveur LDAP prend en charge cette fonctionnalité.

Si vous utilisez un répertoire dans lequel un identificateur unique est hello ancre hello conditions suivantes doivent également être disponibles (pour plus d’informations, consultez hello [configurer des points d’ancrage](#configure-anchors) section) :  
`1.3.6.1.4.1.4203.1.5.1` Tous les attributs opérationnels

Si le répertoire de hello a plus d’objets que ce qui peut tenir dans un seul appel toohello annuaire, il est recommandé toouse pagination. Pour la pagination toowork, vous devez une des options suivantes de hello :

**Option 1 :**  
`1.2.840.113556.1.4.319` pagedResultsControl

**Option 2 :**  
`2.16.840.1.113730.3.4.9` VLVControl  
`1.2.840.113556.1.4.473` SortControl

Si les deux options sont activées dans la configuration du connecteur hello, pagedResultsControl est utilisé.

`1.2.840.113556.1.4.417` ShowDeletedControl

ShowDeletedControl est uniquement utilisé avec hello USNChanged delta importer méthode toobe toosee en mesure de supprimer des objets.

connecteur de Hello tente d’options hello toodetect présentes sur le serveur de hello. Si les options hello ne peut pas être détectées, un avertissement est présent sur la page Global de hello dans Propriétés du connecteur hello. Pas de tous les serveurs LDAP présentes tous les contrôles/fonctionnalités qu’ils prennent en charge et même si cet avertissement s’affiche, hello connecteur peuvent fonctionner sans problème.

### <a name="delta-import"></a>Importation différentielle
L’importation différentielle est disponible uniquement lorsqu’un répertoire pris en charge a été détecté. Hello méthodes suivantes est actuellement utilisé :

* Accesslog LDAP. Voir [http://www.openldap.org/doc/admin24/overlays.html#Access Logging](http://www.openldap.org/doc/admin24/overlays.html#Access Logging)
* Changelog LDAP. Voir [http://tools.ietf.org/html/draft-good-ldap-changelog-04](http://tools.ietf.org/html/draft-good-ldap-changelog-04)
* Horodatage. Pour/NetIQ de Novell eDirectory, tooget de date/heure dernière hello connecteur utilise créé et mis à jour des objets. / NetIQ de Novell eDirectory ne fournit pas d’équivalent signifie que les objets de tooretrieve supprimé. Cette option peut également être utilisée si aucune autre méthode d’importation delta n’est actif sur le serveur LDAP de hello. Cette option n’est pas en mesure de tooimport supprimé objets.
* USNChanged. Consulter : [https://msdn.microsoft.com/library/ms677627.aspx](https://msdn.microsoft.com/library/ms677627.aspx)

### <a name="not-supported"></a>Non pris en charge
Hello suivant les fonctionnalités LDAP n’est pas prises en charge :

* Références LDAP entre serveurs (RFC 4511/4.1.10)

## <a name="create-a-new-connector"></a>Créer un connecteur
tooCreate un connecteur LDAP générique, dans **Service de synchronisation** sélectionnez **Agent de gestion** et **créer**. Sélectionnez hello **LDAP générique (Microsoft)** connecteur.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericldap/createconnector.png)

### <a name="connectivity"></a>Connectivité
Sur la page de connectivité hello, vous devez spécifier hello hôte, Port et informations de liaison. Selon lequel liaison est sélectionné, d’autres informations peuvent être fournies dans les sections suivantes de hello.

![Connectivité](./media/active-directory-aadconnectsync-connector-genericldap/connectivity.png)

* paramètre de délai de connexion Hello est utilisé uniquement pour le premier serveur de toohello connexion hello lors de la détection de schéma de hello.
* Si la liaison est anonyme, ni le nom d’utilisateur/mot de passe ni les certificats ne sont utilisés.
* Pour les autres liaisons, entrez les informations dans les champs de nom d’utilisateur/mot de passe ou sélectionnez un certificat.
* Si vous utilisez Kerberos tooauthenticate, fournissent également hello domaine ou du domaine de l’utilisateur de hello.

Hello **alias d’attribut** zone de texte est utilisée pour les attributs définis dans le schéma hello avec la syntaxe RFC4522. Ces attributs ne peuvent pas être détectées lors de la détection de schéma et hello connecteur doit aider tooidentify ces attributs. Par exemple hello suivantes doivent être entrés dans hello attribut alias boîte toocorrectly identifier attribut userCertificate de hello comme un attribut binaire :

`userCertificate;binary`

Hello Voici un exemple de la manière dont cette configuration pourrait ressembler à :

![Connectivité](./media/active-directory-aadconnectsync-connector-genericldap/connectivityattributes.png)

Sélectionnez hello **incluent des attributs opérationnels dans le schéma** tooalso de case à cocher Inclure les attributs créés par le serveur de hello. Notamment les attributs tels que lorsque les objets hello a été créé et dernière mise à jour.

Sélectionnez **inclut les attributs extensibles schéma** si les objets extensibles (RFC4512/4.3) sont utilisés et l’activation de cette option permet à chaque toobe attribut utilisé sur tous les objets. Cette option permet de schéma de hello très volumineux, sauf si l’annuaire connecté de hello est à l’aide de cette recommandation de hello fonctionnalité est option de hello tookeep désactivée.

### <a name="global-parameters"></a>Paramètres globaux
Sur la page de paramètres globaux de hello, vous configurez journal des modifications hello DN toohello delta et autres fonctionnalités LDAP. page de Hello est prérempli avec les informations de hello fournies par le serveur LDAP de hello.

![Connectivité](./media/active-directory-aadconnectsync-connector-genericldap/globalparameters.png)

section supérieure de Hello affiche des informations fournies par le serveur de hello lui-même, telles que nom hello du serveur de hello. Hello connecteur vérifie également que les contrôles obligatoires hello sont présents dans hello DSE racine. Si tel n’est pas le cas, un avertissement s’affiche. Certains répertoires LDAP ne répertorient pas toutes les fonctions hello DSE racine et il est possible que hello fonctionnement du connecteur sans problème, même si un avertissement s’affiche.

Hello **prise en charge des contrôles** cases à cocher contrôlent le comportement de hello pour certaines opérations :

* Si la suppression de l’arborescence est sélectionnée, une hiérarchie est supprimée avec un appel LDAP. Avec la suppression de l’arborescence a désélectionné, connecteur de hello effectue une suppression récursive si nécessaire.
* Avec des résultats paginés sélectionnés, hello connecteur effectue une importation paginée avec taille hello spécifié sur les étapes de hello exécuter.
* Hello VLVControl et SortControl donnée une autre toohello pagedResultsControl tooread à partir de l’annuaire LDAP de hello.
* Si les trois options (pagedResultsControl, VLVControl et SortControl) sont désélectionnées hello connecteur importe ensuite tous les objets en une seule opération, ce qui risque d’échouer s’il s’agit d’un répertoire volumineux.
* ShowDeletedControl est utilisé uniquement lorsque la méthode d’importation Delta hello est USNChanged.

journal des modifications Hello DN est le contexte de nommage hello utilisé par le journal des modifications delta hello, par exemple **cn = journal des modifications**. Cette valeur doit être spécifié d’importation de toobe toodo en mesure de delta.

Hello Voici une liste par défaut de journal des modifications DNs :

| Répertoire | Journal des modifications différentielles |
| --- | --- |
| Microsoft AD LDS et AD GC |Détecté automatiquement USNChanged. |
| Apache Directory Server |Non disponible |
| Directory 389 |Journal des modifications Par défaut la valeur toouse : **cn = journal des modifications** |
| IBM Tivoli DS |Journal des modifications Par défaut la valeur toouse : **cn = journal des modifications** |
| Isode Directory |Journal des modifications Par défaut la valeur toouse : **cn = journal des modifications** |
| Novell/NetIQ eDirectory |Non disponible Horodatage. Hello connecteur utilise dernière date/heure de mise à jour tooget ajoutés et mis à jour des enregistrements. |
| DJ/DS Open |Journal des modifications  Par défaut la valeur toouse : **cn = journal des modifications** |
| LDAP Open |Journal d’accès. Par défaut la valeur toouse : **cn = accesslog** |
| Oracle DSEE |Journal des modifications Par défaut la valeur toouse : **cn = journal des modifications** |
| RadiantOne VDS |Répertoire virtuel. Dépend de hello annuaire connecté tooVDS. |
| Sun One Directory Server |Journal des modifications Par défaut la valeur toouse : **cn = journal des modifications** |

attribut de mot de passe Hello est nom hello Hello d’attribut hello connecteur doit utiliser le mot de passe tooset hello dans les opérations de jeu de mot de passe et de modification de mot de passe.
Cette valeur par défaut est défini trop**userPassword** mais peut être modifié si nécessaire, pour un système particulier de LDAP.

Dans la liste des partitions supplémentaires hello, il s’agit des espaces de noms supplémentaires possibles tooadd pas automatiquement détecté. Par exemple, ce paramètre peut être utilisé si plusieurs serveurs composent un cluster logique, qui doit être importé à hello même temps. Comme Active Directory peut avoir plusieurs domaines dans une forêt, mais tous les domaines partagent un schéma, hello identiques peuvent être simulés en entrant les espaces de noms supplémentaires hello dans cette zone. Chaque espace de noms peut importer à partir de différents serveurs et est plus configuré sur la page Configurer des Partitions et des hiérarchies de hello. Utilisez Ctrl + Entrée tooget une nouvelle ligne.

### <a name="configure-provisioning-hierarchy"></a>Configurer la hiérarchie de l’approvisionnement
Cette page est utilisé toomap hello DN composant, par exemple unité d’organisation, toohello type d’objet qui doit être configuré, par exemple organizationalUnit.

![Hiérarchie d’approvisionnement](./media/active-directory-aadconnectsync-connector-genericldap/provisioninghierarchy.png)

En configurant la hiérarchie de configuration, vous pouvez configurer hello connecteur tooautomatically créer une structure si nécessaire. Par exemple, s’il existe un espace de noms dc = contoso, dc = com et un nouveau cn d’objet = Joe, ou = Seattle, c = US, dc = contoso, dc = com est configuré, puis hello connecteur peut créer un objet de pays de type pour les États-Unis et une unité d’organisation pour Seattle si ceux-ci sont déjà pas présent dans le répertoire de hello.

### <a name="configure-partitions-and-hierarchies"></a>Configurer des partitions et des hiérarchies
Sur la page de partitions et des hiérarchies hello, sélectionnez tous les espaces de noms avec des objets que vous envisagez tooimport et l’exportation.

![Partitions](./media/active-directory-aadconnectsync-connector-genericldap/partitions.png)

Pour chaque espace de noms, il est également les paramètres de connectivité tooconfigure possibles qui remplacent les valeurs hello spécifiées sur l’écran de connectivité hello. Si ces valeurs sont laissées vides par défaut tootheir, des informations à partir de l’écran de connectivité hello hello sont utilisées.

Il est également possible de tooselect les conteneurs et les unités d’organisation hello connecteur doit importer et exporter vers.

Lorsque vous effectuez une recherche, que cette opération est effectuée sur tous les conteneurs dans la partition de hello. Dans le cas où il existe un grand nombre de conteneurs ce comportement entraîne une dégradation des tooperformance.

>[!NOTE]
À compter de toohello de mise à jour de mars 2017 hello LDAP générique connecteur recherche peut être limitée dans les conteneurs de portée tooonly hello sélectionné. Cela est possible en sélectionnant la case à cocher de hello « Recherche uniquement dans les conteneurs sélectionnés » comme indiqué dans l’image hello ci-dessous.

![Rechercher uniquement dans les conteneurs sélectionnés](./media/active-directory-aadconnectsync-connector-genericldap/partitions-only-selected-containers.png)

### <a name="configure-anchors"></a>Configuration de points d’ancrage
Cette page a toujours une valeur préconfigurée et ne peut pas être modifiée. Si le fournisseur du serveur hello a été identifiée, point d’ancrage hello peut être remplie avec un attribut immuable, pourquoi exemple GUID pour un objet. Si elle n’a pas été détectée ou est connu toonot ont un attribut immuable, puis connecteur de hello utilise dn (nom unique) en tant que point d’ancrage hello.

![Points d’ancrage](./media/active-directory-aadconnectsync-connector-genericldap/anchors.png)


Hello Voici une liste de serveurs LDAP et ancrage hello utilisé :

| Répertoire | Attribut d’ancrage |
| --- | --- |
| Microsoft AD LDS et AD GC |objectGUID |
| Serveur d’annuaire 389 |dn |
| Apache Directory |dn |
| IBM Tivoli DS |dn |
| Isode Directory |dn |
| Novell/NetIQ eDirectory |GUID |
| DJ/DS Open |dn |
| LDAP Open |dn |
| Oracle ODSEE |dn |
| RadiantOne VDS |dn |
| Sun One Directory Server |dn |

## <a name="other-notes"></a>Autres remarques
Cette section fournit des informations des aspects spécifiques toothis connecteur ou pour d’autres raisons tooknow important.

### <a name="delta-import"></a>Importation différentielle
filigrane de delta Hello dans LDAP Open est date/heure UTC. Pour cette raison, les horloges de hello entre le Service de synchronisation FIM et hello LDAP ouverts doivent être synchronisées. Si ce n’est pas le cas, des entrées dans le journal des modifications delta hello peuvent être omises.

Pour Novell eDirectory, importation de delta hello ne détecte pas les suppressions d’objets. Pour cette raison, il est nécessaire toorun complète importer régulièrement toofind toutes les supprimer les objets.

Pour journal qui est basée sur la date/heure de modification de répertoires avec un delta, il est fortement recommandé de toorun une importation intégrale à des moments périodiques. Ce processus autorise toofind de moteur de synchronisation hello et les différences entre le serveur LDAP de hello et ce qui est actuellement dans l’espace de connecteur hello.

## <a name="troubleshooting"></a>Résolution des problèmes
* Pour plus d’informations sur la journalisation de tooenable tootroubleshoot hello connecteur, consultez hello [comment tooEnable le suivi ETW pour les connecteurs](http://go.microsoft.com/fwlink/?LinkId=335731).
