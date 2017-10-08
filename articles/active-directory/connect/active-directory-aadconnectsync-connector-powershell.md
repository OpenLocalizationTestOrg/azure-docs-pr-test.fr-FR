---
title: aaaPowerShell connecteur | Documents Microsoft
description: "Cet article décrit comment le connecteur de tooconfigure Microsoft Windows PowerShell."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 6dba8e34-a874-4ff0-90bc-bd2b0a4199b5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 44ff6b1f53283000b72e15f861e0f86c21afe12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-powershell-connector-technical-reference"></a>Référence technique du connecteur PowerShell Windows
Cet article décrit hello connecteur de Windows PowerShell. article de Hello s’applique toohello suite de produits :

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Nécessité d’utiliser le correctif logiciel 4.1.3671.0 ou une version ultérieure [KB3092178](https://support.microsoft.com/kb/3092178).

MIM2016 et FIM2010R2, hello Connector est disponible en téléchargement à partir de hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-powershell-connector"></a>Vue d’ensemble de hello connecteur de PowerShell
Hello PowerShell connecteur vous permet de service de synchronisation hello toointegrate avec des systèmes externes qui offrent des API basées sur le Windows PowerShell. connecteur de Hello fournit un pont entre les fonctions hello d’agent de gestion extensible connectivity basé sur un appel hello 2 (ECMA2) framework et Windows PowerShell. Pour plus d’informations sur l’infrastructure ECMA hello, consultez hello [Extensible référence de l’Agent de gestion connectivité 2.2](https://msdn.microsoft.com/library/windows/desktop/hh859557.aspx).

### <a name="prerequisites"></a>Composants requis
Avant d’utiliser hello connecteur, vérifiez que vous disposer de hello sur le serveur de synchronisation hello :

* Microsoft .NET 4.5.2 Framework ou version ultérieure
* Windows PowerShell 2.0, 3.0 ou 4.0

stratégie d’exécution Hello sur le serveur du Service de synchronisation hello doit être configuré tooallow hello connecteur toorun les scripts Windows PowerShell. Sauf si les séries de connecteur hello hello scripts sont signées numériquement, configurer la stratégie d’exécution hello en exécutant cette commande :  
`Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`

## <a name="create-a-new-connector"></a>Créer un connecteur
toocreate un connecteur de Windows PowerShell dans le service de synchronisation hello, vous devez fournir une série de scripts Windows PowerShell qui s’exécutent des étapes hello demandés par le service de synchronisation hello. En fonction de la source de données hello vous connectez les fonctionnalités de hello tooand vous avez besoin, vous devez implémenter des scripts hello varie. Cette section décrit chacune des scripts hello qui peut être implémentée et lorsqu’ils sont requis.

Hello Windows PowerShell, le connecteur est conçu toostore de scripts hello au sein de la base de données du Service de synchronisation hello. Bien qu’il soit possible toorun les scripts qui sont stockés sur le système de fichiers hello, il s’agit des corps de hello tooinsert plus facile de chaque script directement dans la configuration du connecteur de toohello.

tooCreate un connecteur de PowerShell, dans **Service de synchronisation** sélectionnez **Agent de gestion** et **créer**. Sélectionnez hello **PowerShell (Microsoft)** connecteur.

![Créer un connecteur](./media/active-directory-aadconnectsync-connector-powershell/createconnector.png)

### <a name="connectivity"></a>Connectivité
Fournir des paramètres de configuration pour la connexion du système distant de tooa. Ces valeurs sont en toute sécurité stockées par hello Service de synchronisation et effectuées des scripts Windows PowerShell tooyour disponibles lors de l’exécution de connecteur de hello.

![Connectivité](./media/active-directory-aadconnectsync-connector-powershell/connectivity.png)

Vous pouvez configurer hello les paramètres de connectivité suivants :

**Connectivité**

| Paramètre | Valeur par défaut | Objectif |
| --- | --- | --- |
| Serveur |<Blank> |Nom du serveur hello connecteur doit se connecter à. |
| Domaine |<Blank> |Domaine de toostore des informations d’identification hello pour une utilisation lors de l’exécution de connecteur de hello. |
| Utilisateur |<Blank> |Nom d’utilisateur de toostore des informations d’identification hello pour une utilisation lors de l’exécution de connecteur de hello. |
| Mot de passe |<Blank> |Mot de passe de toostore des informations d’identification hello pour une utilisation lors de l’exécution de connecteur de hello. |
| Emprunter l’identité du compte de connecteur |False |Lorsque la valeur est true, le service de synchronisation hello s’exécute des scripts Windows PowerShell hello dans le contexte hello d’informations d’identification hello fourni. Lorsque cela est possible, il est recommandé que hello **$Credentials** paramètre est passé de tooeach script est utilisé au lieu de l’emprunt d’identité. Pour plus d’informations sur les autorisations supplémentaires qui sont requis toouse cette option, consultez [une Configuration supplémentaire pour l’emprunt d’identité](#additional-configuration-for-impersonation). |
| Charger le profil utilisateur lors de l’emprunt d’identité |False |Indique le profil d’utilisateur Windows tooload hello d’informations d’identification du connecteur hello lors de l’emprunt d’identité. Si l’utilisateur représenté hello possède un profil itinérant, connecteur de hello ne charge pas le profil itinérant de hello. Pour plus d’informations sur les autorisations supplémentaires qui sont requis toouse ce paramètre, consultez [une Configuration supplémentaire pour l’emprunt d’identité](#additional-configuration-for-impersonation). |
| Type d’ouverture en cas d’emprunt d’identité |Aucun |Type de connexion pendant l’emprunt d’identité. Pour plus d’informations, consultez hello [dwLogonType] [ dw] documentation. |
| Scripts signés uniquement |False |Si la valeur est true, connecteur de Windows PowerShell hello valide que chaque script possède une signature numérique valide. Si la valeur est false, assurez-vous que la stratégie d’exécution Windows PowerShell du serveur du Service de synchronisation de hello est RemoteSigned ou non restreint. |

**Module commun**  
connecteur de Hello vous permet de toostore un module Windows PowerShell partagé dans la configuration de hello. Lorsque le connecteur de hello exécute un script, hello Windows PowerShell module est extraite système de fichiers toohello afin qu’il puisse être importé par chaque script.

Pour les scripts d’importation, exportation et la synchronisation de mot de passe, module commun de hello est dossier de MAData du connecteur toohello extraits. Pour les scripts de détection de schéma, de Validation, de hiérarchie et de Partition, module commun de hello est dossier extraits toohello % temp%. Dans les deux cas, hello extraits Module commun script est nommé en fonction du paramètre de nom de Script commun Module toohello.

tooload un module appelé FIMPowerShellConnectorModule.psm1 à partir du dossier MAData hello, utilisez hello après l’instruction :`Import-Module (Join-Path -Path [Microsoft.MetadirectoryServices.MAUtils]::MAFolder -ChildPath "FIMPowerShellConnectorModule.psm1")`

tooload un module appelé FIMPowerShellConnectorModule.psm1 à partir du dossier % Temp% hello, utilisez hello après l’instruction :`Import-Module (Join-Path -Path $env:TEMP -ChildPath "FIMPowerShellConnectorModule.psm1")`

**Validation des paramètres**  
Hello Script de Validation est un script Windows PowerShell facultatif qui peut être utilisé tooensure que les paramètres de configuration de connecteur fournis par l’administrateur de hello sont valides. Serveur de validation, les informations d’identification de connexion et les paramètres de connectivité sont des utilisations courantes de script de validation hello. script de validation Hello est appelée après que hello des onglets et des boîtes de dialogue suivants sont modifiés :

* Connectivité
* Paramètres globaux
* Configuration de partition

script de validation Hello reçoit hello après les paramètres du connecteur de hello :

| Nom | Type de données | Description |
| --- | --- | --- |
| ConfigParameterPage |[ConfigParameterPage][cpp] |onglet de configuration Hello ou boîte de dialogue qui a déclenché la demande de validation hello. |
| ConfigParameters |[KeyedCollection][keyk] [string, [ConfigParameter][cp]] |Tableau des paramètres de configuration pour hello connecteur. |
| Informations d'identification |[PSCredential][pscred] |Contient des informations d’identification entrées par l’administrateur de hello sur l’onglet de connectivité hello. |

script de validation Hello doit retourner un pipeline de toohello ParameterValidationResult objet unique.

**Découverte de schéma**  
Hello script de détection de schéma est obligatoire. Ce script retourne des types d’objets hello, des attributs et des contraintes de l’attribut que hello que service de synchronisation utilise lors de la configuration des règles de flux d’attribut. Hello script de détection de schéma est exécutée lors de la création du connecteur et remplit les schémas du connecteur hello. Il est également utilisé par hello action Actualiser le schéma Bonjour Synchronization Service Manager.

script de découverte de schéma Hello reçoit hello après les paramètres du connecteur de hello :

| Nom | Type de données | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk] [string, [ConfigParameter][cp]] |Tableau des paramètres de configuration pour hello connecteur. |
| Informations d'identification |[PSCredential][pscred] |Contient des informations d’identification entrées par l’administrateur de hello sur l’onglet de connectivité hello. |

script de Hello doit retourner une seule [schéma] [ schema] toohello pipeline d’objet. objet de schéma Hello est composé de [SchemaType] [ schemaT] objets qui représentent des types d’objet (par exemple : utilisateurs et groupes). objet de SchemaType Hello conserve une collection de [SchemaAttribute] [ schemaA] les objets qui représentent les attributs hello (par exemple : prénom, nom et adresse postale) du type de hello.

**Paramètres supplémentaires**  
En outre toohello des paramètres de configuration standard, vous pouvez définir des paramètres supplémentaires de configuration personnalisée instance toohello spécifique de hello connecteur. Ces paramètres peuvent être spécifiés au connecteur hello, partition, ou les niveaux d’étape d’exécution et accessible à partir de script Windows PowerShell appropriée de hello. Paramètres de configuration personnalisés peuvent être stockées dans la base de données du Service de synchronisation hello au format texte brut, ou ils peuvent être chiffrés. Service de synchronisation de Hello chiffre et déchiffre les paramètres de configuration sécurisés à la demande automatiquement.

paramètres de configuration personnalisés toospecify, nom hello distincts de chaque paramètre avec une virgule (,).

tooaccess les paramètres de configuration personnalisé à partir d’un script, vous devez le suffixe nom hello avec un trait de soulignement ( \_ ) et la portée de hello du paramètre hello (Global, la Partition ou RunStep). Par exemple, tooaccess hello paramètre FileName Global, utilisez cet extrait de code :`$ConfigurationParameters["FileName_Global"].Value`

### <a name="capabilities"></a>Fonctionnalités
onglet de capacités Hello Hello Concepteur de l’Agent de gestion définit les fonctionnalités du connecteur de hello et comportement de hello. Impossible de modifier les sélections de Hello sous cet onglet lorsque hello connecteur a été créé. Ce tableau répertorie les paramètres de capacité hello.

![Fonctionnalités](./media/active-directory-aadconnectsync-connector-powershell/capabilities.png)

| Fonctionnalité | Description |
| --- | --- |
| [Style de nom unique][dnstyle] |Indique si le connecteur de hello prend en charge les noms uniques et par conséquent, le style. |
| [Type d’exportation][exportT] |Détermine le type hello d’objets qui sont présentés toohello script d’exportation. <li>AttributeReplace – inclut hello complète ensemble de valeurs pour un attribut à valeurs multiples lorsque hello attribut change.</li><li>AttributeUpdate – inclut uniquement hello deltas tooa attribut à valeurs multiples lorsque hello attribut change.</li><li>MultivaluedReferenceAttributeUpdate - contient un ensemble complet de valeurs d’attributs à valeurs multiples sans référence et uniquement pour les écarts des attributs de référence à valeurs multiples.</li><li>ObjectReplace – inclut tous les attributs d’un objet en cas de modification d’attribut</li> |
| [Normalisation des données][DataNorm] |Indique les attributs de point d’ancrage toonormalize hello Service de synchronisation avant qu’ils sont fournis tooscripts. |
| [Confirmation d’objet][oconf] |Configure hello en attente de comportement d’importation Bonjour Service de synchronisation. <li>Normal – par défaut qui attend que toutes les modifications exporté toobe a été confirmé par l’importation</li><li>NoDeleteConfirmation – lorsqu’un objet est supprimé, aucune importation en attente n’est générée.</li><li>NoAddAndDeleteConfirmation – lorsqu’un objet est créé ou supprimé, aucune importation en attente n’est générée.</li> |
| Utiliser le nom unique en tant que point d’ancrage |Si hello Style de nom unique tooLDAP, attribut d’ancrage hello pour l’espace de connecteur hello est également nom_unique hello. |
| Opérations simultanées de plusieurs connecteurs |Lorsqu’elle est activée, plusieurs connecteurs de Windows PowerShell peuvent s’exécuter simultanément. |
| Partitions |Lorsqu’elle est activée, le connecteur de hello prend en charge plusieurs partitions et découverte de partition. |
| Hiérarchie |Lorsqu’elle est activée, le connecteur de hello prend en charge une structure hiérarchique de style LDAP. |
| Activer l’importation |Lorsqu’elle est activée, le connecteur de hello importe des données via des scripts d’importation. |
| Activer l’importation d’écart |Lorsqu’elle est activée, le connecteur de hello peut demander deltas de hello importer des scripts. |
| Activer l’exportation |Lorsqu’elle est activée, le connecteur de hello exporte des données via des scripts d’exportation. |
| Activer l’exportation complète |Lorsqu’elle est activée, hello exporter exportation espace de connecteur entière hello de la prise en charge des scripts. toouse que cette option, activez exporter doit également être activée. |
| Aucune valeur de référence dans le premier transfert d’exportation |Lorsqu’elle est activée, les attributs de référence sont exportés lors d’un deuxième transfert d’exportation. |
| Activer renommer l’objet |Lorsqu’elle est activée, les noms uniques peuvent être modifiés. |
| Supprimer-Ajouter en remplacement |Lorsqu’elle est activée, les opérations supprimer, ajouter sont exportées en tant que remplacement. |
| Activer les opérations de mot de passe |Lorsqu’elle est activée, les scripts de synchronisation de mot de passe sont pris en charge. |
| Activer l’exportation de mot de passe lors d’un premier passage |Lorsqu’elle est activée, les mots de passe défini lors de la configuration sont exportés lors de la création d’objet de hello. |

### <a name="global-parameters"></a>Paramètres globaux
onglet Paramètres globaux de Hello Bonjour Concepteur de l’Agent de gestion vous permet de tooconfigure hello Windows PowerShell scripts qui sont exécutés par le connecteur de hello. Vous pouvez également configurer des valeurs globales pour les paramètres de configuration personnalisés définis sur l’onglet de connectivité hello.

**Détection de partition**  
Une partition est un espace de noms distinct au sein d’un seul schéma partagé. Par exemple, dans Active Directory, chaque domaine est une partition d’une forêt. Une partition est le regroupement logique de hello pour importer et exporter des opérations. L’importation et l’exportation se trouvent dans un environnement de partition et toutes les opérations ont lieu dans ce contexte. Les partitions sont censées toorepresent une hiérarchie dans l’annuaire LDAP. nom unique de Hello d’une partition est utilisé dans tooverify d’importation que toutes les renvoyées objets se trouvent dans la portée de hello d’une partition. nom unique de la partition Hello est également utilisé lors de la configuration à partir de hello métaverse toohello connecteur espace toodetermine hello partition de qu'un objet doit être associé lors de l’exportation.

script de découverte de partition Hello reçoit hello après les paramètres du connecteur de hello :

| Nom | Type de données | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tableau des paramètres de configuration pour hello connecteur. |
| Informations d'identification |[PSCredential][pscred] |Contient des informations d’identification entrées par l’administrateur de hello sur l’onglet de connectivité hello. |

Hello script doit retourner un un seul [Partition] [ part] objet ou une liste [T] du pipeline de toohello objets Partition.

**Découverte de la hiérarchie**  
script de découverte de hiérarchie Hello est utilisé uniquement lors de la fonctionnalité de Style de nom unique de hello est LDAP. script de Hello est utilisé tooallow vous toobrowse et sélectionnez un ensemble de conteneurs est considérée comme dans ou hors de portée pour importer et exporter des opérations. script de Hello doit fournir uniquement une liste de nœuds qui sont des enfants directs du script de toohello hello racine nœud fourni.

script de découverte de hiérarchie Hello reçoit hello après les paramètres du connecteur de hello :

| Nom | Type de données | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tableau des paramètres de configuration pour hello connecteur. |
| Informations d'identification |[PSCredential][pscred] |Contient des informations d’identification entrées par l’administrateur de hello sur l’onglet de connectivité hello. |
| ParentNode |[HierarchyNode][hn] |nœud racine de Hello de hiérarchie hello sous le hello script doit retourner les enfants directs. |

script de Hello doit retourner un un objet de HierarchyNode enfant unique ou une liste [T] du pipeline de toohello objets enfant HierarchyNode.

#### <a name="import"></a>Importer
Les connecteurs qui prennent en charge les opérations d’importation doivent implémenter trois scripts.

**Début de l’importation**  
commencer l’importation Hello script est exécuté au début de hello d’une étape d’importation à exécuter. Pendant cette étape, vous pouvez établir un système de connexion toohello source et effectuer les étapes préparatoires avant l’importation de données à partir de hello connectés système.

commencer l’importation Hello script reçoit hello après les paramètres du connecteur de hello :

| Nom | Type de données | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tableau des paramètres de configuration pour hello connecteur. |
| Informations d'identification |[PSCredential][pscred] |Contient des informations d’identification entrées par l’administrateur de hello sur l’onglet de connectivité hello. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Script de hello informe de type hello d’exécuter l’importation (delta ou full), partition, hiérarchie, filigrane et taille de page attendu. |
| Types |[Schema][schema] |Schéma pour l’espace de connecteur hello qui est importé. |

script de Hello doit retourner une seule [OpenImportConnectionResults] [ oicres] objet toohello pipeline, par exemple :`Write-Output (New-Object Microsoft.MetadirectoryServices.OpenImportConnectionResults)`

**Importer des données**  
script d’importation de données Hello est appelé par le connecteur de hello jusqu'à ce que le script de hello indique qu’il n’y a aucune tooimport plus de données. connecteur de Windows PowerShell Hello a une taille de page d’objets 9 999. Si votre script renvoie plus de 9 999 objets pour importation, vous devez prendre en charge la pagination. expose de connecteur Hello une propriété de données personnalisé que vous pouvez utiliser le magasin de tooa un filigrane afin que chaque hello temps importer le script de données est appelée, votre script reprend l’importation d’objets dans lequel il s’est arrêté.

script d’importation de données Hello reçoit hello après les paramètres du connecteur de hello :

| Nom | Type de données | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tableau des paramètres de configuration pour hello connecteur. |
| Informations d'identification |[PSCredential][pscred] |Contient des informations d’identification entrées par l’administrateur de hello sur l’onglet de connectivité hello. |
| GetImportEntriesRunStep |[ImportRunStep][irs] |Blocages hello filigrane (CustomData) qui peut être utilisé au cours des importations paginées et importe de delta. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Script de hello informe de type hello d’exécuter l’importation (delta ou full), partition, hiérarchie, filigrane et taille de page attendu. |
| Types |[Schema][schema] |Schéma pour l’espace de connecteur hello qui est importé. |

Hello script d’importation de données doit écrire une liste [[CSEntryChange][csec]] pipeline toohello d’objet. Cette collection se compose d’attributs CSEntryChange qui représentent chaque objet importé. Au cours d’une importation intégrale, cette collection doit comporter un jeu complet d’objets CSEntryChange qui dispose de tous les attributs de chaque objet. Lors de l’importation Delta, objet de CSEntryChange hello doit contenir deltas de niveau attribut hello pour chaque tooimport d’objet ou une représentation complète d’objets hello qui ont été modifiés (mode de remplacement).

**Fin de l’importation**  
À fin hello d’importation hello exécuter hello fin importer le script est exécuté. Ce script doit effectuer les tâches de nettoyage sont nécessaires (par exemple, une toosystems et répondre toofailures fermer les connexions).

script d’importation de fin Hello reçoit hello après les paramètres du connecteur de hello :

| Nom | Type de données | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tableau des paramètres de configuration pour hello connecteur. |
| Informations d'identification |[PSCredential][pscred] |Contient des informations d’identification entrées par l’administrateur de hello sur l’onglet de connectivité hello. |
| OpenImportConnectionRunStep |[OpenImportConnectionRunStep][oicrs] |Script de hello informe de type hello d’exécuter l’importation (delta ou full), partition, hiérarchie, filigrane et taille de page attendu. |
| CloseImportConnectionRunStep |[CloseImportConnectionRunStep][cecrs] |Script de hello informe de la raison hello importation de hello a été interrompue. |

script de Hello doit retourner une seule [CloseImportConnectionResults] [ cicres] objet toohello pipeline, par exemple :`Write-Output (New-Object Microsoft.MetadirectoryServices.CloseImportConnectionResults)`

#### <a name="export"></a>Exportation
Architecture d’importation toohello identiques du connecteur de hello, les connecteurs qui prennent en charge d’exportation doivent implémenter trois scripts.

**Début de l’exportation**  
Hello commencer l’exportation de script est exécuté au début de hello d’une étape d’exportation. Au cours de cette étape, vous pouvez établir un système de source de connexion toohello et effectuer toutes les étapes préparatoires avant l’exportation de données toohello connecté système.

commencer l’exportation Hello script reçoit hello après les paramètres du connecteur de hello :

| Nom | Type de données | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tableau des paramètres de configuration pour hello connecteur. |
| Informations d'identification |[PSCredential][pscred] |Contient des informations d’identification entrées par l’administrateur de hello sur l’onglet de connectivité hello. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Script de hello informe de type hello de d’exportation (delta ou full), partition, hiérarchie et la taille de page attendue. |
| Types |[Schema][schema] |Schéma pour l’espace de connecteur hello exporté. |

script de Hello ne doit pas retourner tout pipeline toohello de sortie.

**Exporter les données**  
Hello Service de synchronisation appelle script d’exporter des données hello aussi souvent que toutes les exportations en attente n’est nécessaire tooprocess. Si l’espace de connecteur hello possède plusieurs exportations en attente que hello la taille de la page du connecteur, exportation hello de script de données peut être appelée plusieurs fois et éventuellement plusieurs fois pour hello même objet.

script de données d’exportation Hello reçoit hello après les paramètres du connecteur de hello :

| Nom | Type de données | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tableau des paramètres de configuration pour hello connecteur. |
| Informations d'identification |[PSCredential][pscred] |Contient des informations d’identification entrées par l’administrateur de hello sur l’onglet de connectivité hello. |
| CSEntries |IList[CSEntryChange][csec] |Liste de tous les objets d’espace connecteur hello avec attente toobe exportations traités au cours de cette étape. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Script de hello informe de type hello de d’exportation (delta ou full), partition, hiérarchie et la taille de page attendue. |
| Types |[Schema][schema] |Schéma pour l’espace de connecteur hello exporté. |

Hello script de données d’exportation doit retourner un [PutExportEntriesResults] [ peeres] toohello pipeline d’objet. Cet objet ne nécessite pas de tooinclude les informations de résultat pour chaque connecteur exporté, sauf si une erreur ou un attribut d’ancrage toohello modification se produit. Par exemple, tooreturn un pipeline de toohello PutExportEntriesResults objet :`Write-Output (New-Object Microsoft.MetadirectoryServices.PutExportEntriesResults)`

**Fin d’exportation**  
À la conclusion de l’exportation de hello hello exécuter, hello toorun de script exporter de fin. Ce script doit effectuer les tâches de nettoyage sont nécessaires (par exemple, une toosystems et répondre toofailures fermer les connexions).

script d’exportation Hello fin reçoit hello après les paramètres du connecteur de hello :

| Nom | Type de données | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tableau des paramètres de configuration pour hello connecteur. |
| Informations d'identification |[PSCredential][pscred] |Contient des informations d’identification entrées par l’administrateur de hello sur l’onglet de connectivité hello. |
| OpenExportConnectionRunStep |[OpenExportConnectionRunStep][oecrs] |Script de hello informe de type hello de d’exportation (delta ou full), partition, hiérarchie et la taille de page attendue. |
| CloseExportConnectionRunStep |[CloseExportConnectionRunStep][cecrs] |Script de hello informe de la raison hello exportation de hello a été interrompue. |

script de Hello ne doit pas retourner tout pipeline toohello de sortie.

#### <a name="password-synchronization"></a>Synchronisation du mot de passe
Les connecteurs PowerShell Windows peuvent servir de cible pour les modifications/réinitialisations du mot de passe.

script de mot de passe Hello reçoit hello après les paramètres du connecteur de hello :

| Nom | Type de données | Description |
| --- | --- | --- |
| ConfigParameters |[KeyedCollection][keyk][string, [ConfigParameter][cp]] |Tableau des paramètres de configuration pour hello connecteur. |
| Informations d'identification |[PSCredential][pscred] |Contient des informations d’identification entrées par l’administrateur de hello sur l’onglet de connectivité hello. |
| Partition |[Partition][part] |Partition d’annuaire hello CSEntry est dans. |
| CSEntry |[CSEntry][cse] |Entrée d’espace de connecteur d’objet hello a reçu une modification de mot de passe ou de la réinitialisation. |
| OperationType |String |Indique si l’opération de hello est une réinitialisation (**SetPassword**) ou une modification (**ChangePassword**). |
| PasswordOptions |[PasswordOptions][pwdopt] |Indicateurs qui spécifient les hello destiné le comportement de réinitialisation de mot de passe. Ce paramètre est disponible uniquement si le type d’opération est défini sur **SetPassword**. |
| OldPassword |String |Rempli avec ancien mot de passe l’objet hello pour les modifications de mot de passe. Ce paramètre est disponible uniquement si le type d’opération est **ChangePassword**. |
| NewPassword |String |Rempli avec nouveau mot de passe l’objet hello que les scripts de hello doivent définir. |

Hello script de mot de passe est non attendu tooreturn tout pipeline Windows PowerShell de toohello résultats. Si une erreur se produit dans le script de mot de passe hello, script de hello doit lever l’une des hello suivant exceptions tooinform hello Service de synchronisation sur le problème de hello :

* [PasswordPolicyViolationException] [ pwdex1] – levée si un mot de passe hello ne remplit pas la stratégie de mot de passe hello dans le système de hello connecté.
* [PasswordIllFormedException] [ pwdex2] – levée si le mot de passe hello n’est pas acceptable pour le système de hello connecté.
* [PasswordExtension] [ pwdex3] – levé pour toutes les autres erreurs dans le script de mot de passe hello.

## <a name="sample-connectors"></a>Exemple de connecteurs
Pour une vue d’ensemble complète des connecteurs d’exemples hello, consultez [exemple connecteur Windows PowerShell de Collection de connecteur][samp].

## <a name="other-notes"></a>Autres remarques
### <a name="additional-configuration-for-impersonation"></a>Configuration supplémentaire pour l’emprunt d’identité
Grant hello utilisateur avec emprunt d’identité hello autorisations sur le serveur du Service de synchronisation hello suivantes :

Toohello d’accès en lecture suivant des clés de Registre :

* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Software\Microsoft\PowerShell
* HKEY_USERS\\[SynchronizationServiceServiceAccountSID]\Environment

hello toodetermine identificateur de sécurité (SID) du compte de service de Service de synchronisation hello, exécutez hello suivant de commandes PowerShell :

```
$account = New-Object System.Security.Principal.NTAccount "<domain>\<username>"
$account.Translate([System.Security.Principal.SecurityIdentifier]).Value
```

Toohello d’accès en lecture suivant des dossiers système de fichiers :

* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\Extensions
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\ExtensionsCache
* %ProgramFiles%\Microsoft Forefront Identity Manager\2010\Synchronization Service\MaData\\{ConnectorName}

Remplacez nom hello du connecteur de Windows PowerShell hello d’espace réservé de hello {ConnectorName}.

## <a name="troubleshooting"></a>Résolution des problèmes
* Pour plus d’informations sur la journalisation de tooenable tootroubleshoot hello connecteur, consultez hello [comment tooEnable le suivi ETW pour les connecteurs](http://go.microsoft.com/fwlink/?LinkId=335731).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[cpp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameterpage.aspx
[keyk]: https://msdn.microsoft.com/library/ms132438.aspx
[cp]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.configparameter.aspx
[pscred]: https://msdn.microsoft.com/library/system.management.automation.pscredential.aspx
[schema]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schema.aspx
[schemaT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schematype.aspx
[schemaA]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.schemaattribute.aspx
[dnstyle]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.madistinguishednamestyle.aspx
[exportT]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maexporttype.aspx
[DataNorm]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.manormalizations.aspx
[oconf]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.maobjectconfirmation.aspx
[dw]: https://msdn.microsoft.com/library/windows/desktop/aa378184.aspx
[part]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.partition.aspx
[hn]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.hierarchynode.aspx
[oicrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionrunstep.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[oicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openimportconnectionresults.aspx
[cecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeexportconnectionrunstep.aspx
[cicres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.closeimportconnectionresults.aspx
[oecrs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.openexportconnectionrunstep.aspx
[irs]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.importrunstep.aspx
[cse]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentry.aspx
[csec]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.csentrychange.aspx
[peeres]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.putexportentriesresults.aspx
[pwdopt]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordoptions.aspx
[pwdex1]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordpolicyviolationexception.aspx
[pwdex2]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordillformedexception.aspx
[pwdex3]: https://msdn.microsoft.com/library/windows/desktop/microsoft.metadirectoryservices.passwordextensionexception.aspx
[samp]: http://go.microsoft.com/fwlink/?LinkId=394291
