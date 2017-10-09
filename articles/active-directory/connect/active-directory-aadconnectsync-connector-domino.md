---
title: aaaLotus Domino connecteur | Documents Microsoft
description: "Cet article décrit comment Lotus Domino connecteur tooconfigure Microsoft."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: e07fd469-d862-470f-a3c6-3ed2a8d745bf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: affef1fec91eb39f7e91ec274fdd1b3a9c4a32fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="lotus-domino-connector-technical-reference"></a>Référence technique du connecteur Lotus Domino
Cet article décrit hello connecteur pour Lotus Domino. article de Hello s’applique toohello suite de produits :

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Nécessité d’utiliser le correctif logiciel 4.1.3671.0 ou une version ultérieure [KB3092178](https://support.microsoft.com/kb/3092178).

MIM2016 et FIM2010R2, hello Connector est disponible en téléchargement à partir de hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

## <a name="overview-of-hello-lotus-domino-connector"></a>Vue d’ensemble de hello connecteur pour Lotus Domino
Hello Lotus Domino connecteur vous permet de service de synchronisation hello toointegrate avec le serveur de Lotus Domino d’IBM.

À partir d’un point de vue global, hello suivant les fonctionnalités est prises en charge par la version actuelle de hello du connecteur de hello :

| Fonctionnalité | Support |
| --- | --- |
| Source de données connectée |Serveur :  <li>Lotus Domino 8.5.x</li><li>Lotus Domino 9.x</li>Client :<li>Lotus Domino 8.5.x</li><li>Lotus Notes 9.x</li> |
| Scénarios |<li>Gestion du cycle de vie des objets</li><li>Gestion des groupes</li><li>Gestion des mots de passe</li> |
| Opérations |<li>Importation complète et différentielle</li><li>Exportation</li><li>Définition et modification du mot de passe HTTP</li> |
| Schéma |<li>Personne (utilisateurs itinérants, contacts (personnes sans certificat))</li><li>Groupe</li><li>Ressources (ressource, salle, réunion en ligne)</li><li>Base courrier en arrivée</li><li>Découverte dynamique des attributs pour les objets pris en charge</li> |

connecteur de Lotus Domino Hello utilise hello Lotus Notes client toocommunicate avec serveur Lotus Domino. En raison de cette dépendance, un Client pris en charge de Lotus Notes doit être installé sur le serveur de synchronisation hello. Hello la communication entre le client de hello et le serveur de hello est implémentée via l’interface de Lotus Notes .NET Interop (Interop.domino.dll) hello. Cette interface facilite la communication hello entre la plateforme de Microsoft.NET hello et client Lotus Notes et prend en charge les accès tooLotus Domino documents et vues. Pour l’importation de delta, il est également possible que l’interface native hello C++ est utilisée (selon la méthode d’importation hello sélectionné delta).

### <a name="prerequisites"></a>Composants requis
Avant d’utiliser hello connecteur, vérifiez que vous avez hello suivant les composants requis sur le serveur de synchronisation hello :

* Microsoft .NET 4.5.2 Framework ou version ultérieure
* client de Lotus Notes Hello doit être installé sur votre serveur de synchronisation
* Hello connecteur pour Lotus Domino nécessite hello par défaut Lotus Domino LDAP schéma de base de données (schema.nsf) toobe présent sur le serveur d’annuaire Domino hello. Si elle n’est pas présent, vous pouvez l’installer en exécutant ou redémarrer le service LDAP hello sur le serveur de Domino hello.

### <a name="connected-data-source-permissions"></a>Autorisations de la source de données connectée
tooperform tout Hello pris en charge les tâches dans le connecteur de Lotus Domino, vous devez être membre des groupes suivants :

* Administrateurs avec accès total
* Administrateurs
* Administrateurs de base de données

Hello tableau suivant répertorie les autorisations hello qui sont requises pour chaque opération :

| Opération | Droits d’accès |
| --- | --- |
| Importer |<li>Lire les documents publics</li><li> Accès administrateur complet (lorsque vous êtes membre du groupe d’administrateurs un accès complet, vous avez automatiquement accès effectif de hello tooin ACL.)</li> |
| Exporter et définir le mot de passe |Accès effectif :  <li>Création de documents</li><li>Supprimer des documents</li><li>Lire les documents publics</li><li>Écrire des documents publics</li><li>Répliquer ou copier des documents</li>Pour les opérations d’exportation, vous devez également hello suivant des rôles : <li>CreateResource</li><li>GroupCreator</li><li>GroupModifier</li><li>UserCreator</li><li>UserModifier</li> |

### <a name="direct-operations-and-adminp"></a>Opérations directes et AdminP
Les opérations accédez directement toohello Domino directory ou via hello AdminP traitent. Hello tableaux suivants répertorient tous les objets pris en charge, les opérations et, le cas échéant, hello liés de méthode d’implémentation :

**Carnet d’adresses principal**

| Object | Créer | Mettre à jour | Supprimer |
| --- | --- | --- | --- |
| Personne |AdminP |Directement |AdminP |
| Groupe |AdminP |Directement |AdminP |
| MailInDB |Directement |Directement |Directement |
| Ressource |AdminP |Directement |AdminP |

**Carnet d’adresses secondaire**

| Object | Créer | Mettre à jour | Supprimer |
| --- | --- | --- | --- |
| Personne |N/A |Directement |Directement |
| Groupe |Directement |Directement |Directement |
| MailInDB |Directement |Directement |Directement |
| Ressource |N/A |N/A |N/A |

Lorsqu’une ressource est créée, un document Notes est créé. De même, lorsqu’une ressource est supprimée, document Notes de publication de hello est supprimé.

### <a name="ports-and-protocols"></a>Ports et protocoles
Le client IBM Lotus Notes et les serveurs Domino communiquent à l’aide d’un appel de procédure distante Notes (NRPC), où NRPC doit utiliser le protocole TCP/IP. numéro de port par défaut Hello est 1352, mais peut être modifié par l’administrateur de Domino hello.

### <a name="not-supported"></a>Non pris en charge
Hello opérations suivantes n’est pas pris en charge par la version actuelle de hello du connecteur Lotus Domino de hello :

* Déplacer des boîtes aux lettres entre des serveurs.

## <a name="create-a-new-connector"></a>Créer un connecteur
### <a name="client-software-installation-and-configuration"></a>Installation et configuration du logiciel client
Lotus Notes doivent être installés sur le serveur de hello **avant** hello connecteur est installé.

Lors de l’installation, assurez-vous de choisir **Single User Install**. par défaut de Hello **multi-utilisateur installer** ne fonctionne pas.  
![Notes1](./media/active-directory-aadconnectsync-connector-domino/notes1.png)

Sur la page de composants hello, installez uniquement hello requis des fonctionnalités de Lotus Notes et **ouverture de session unique Client**. Ouverture de session unique est requis pour hello connecteur toobe en mesure de toolog sur le serveur de toohello Domino.  
![Notes2](./media/active-directory-aadconnectsync-connector-domino/notes2.png)

**Remarque :** démarrer Lotus Notes une fois qu’un utilisateur qui se trouve sur hello même serveur que hello compte que vous utilisez comme compte de service du connecteur de hello. Assurez-vous également que client de Lotus Notes tooclose hello sur le serveur de hello. Il ne peut pas être en cours d’exécution à hello hello temps même connecteur tente de serveur de tooconnect toohello Domino.

### <a name="create-connector"></a>Créer un connecteur
tooCreate un connecteur Lotus Domino, dans **Service de synchronisation** sélectionnez **Agent de gestion** et **créer**. Sélectionnez hello **Lotus Domino (Microsoft)** connecteur.  
![CreateConnector](./media/active-directory-aadconnectsync-connector-domino/createconnector.png)

Si votre version de service de synchronisation offre hello capacité tooconfigure **Architecture**, assurez-vous que le connecteur de hello est toorun de valeur par défaut tooits dans **processus**.

### <a name="connectivity"></a>Connectivité
Sur la page de connectivité hello, vous devez spécifier le nom du serveur Lotus Domino hello et entrez les informations d’identification d’ouverture de session de hello.  
![Connectivité](./media/active-directory-aadconnectsync-connector-domino/connectivity.png)

Hello propriété Domino Server prend en charge deux formats de nom du serveur hello :

* ServerName
* ServerName/DirectoryName

Hello **nom_serveur/Nom_répertoire** format est le format par défaut de hello pour cet attribut, car il fournit une réponse plus rapide lorsque les contacts de connecteur hello hello serveur Domino.

Hello fourni UserID fichier est stocké dans la base de données de configuration hello du service de synchronisation hello.

Pour **Delta Import** , vous disposez des options suivantes :

* **None**. Hello connecteur n’effectue aucune importation delta.
* **Add/Update**. importation de delta Hello connecteur fait ajouter et mettre à jour des opérations. Pour la suppression, une opération **Full Import** est requise. Cette opération est à l’aide d’interopérabilité de .net hello.
* **Add/Update/Delete**. importation de delta a Hello connecteur ajouter, mettre à jour et les opérations de suppression. Cette opération est à l’aide des interfaces C++ natives hello.

Dans **Options de schéma** avoir hello options suivantes :

* **Default Schema**. Hello connecteur détecte schéma hello du serveur de Domino hello. Cette sélection est l’option par défaut de hello.
* **DSML-Schema**. Utilisé uniquement si le serveur de Domino hello n’expose pas de schéma de hello. Vous pouvez ensuite créer un fichier DSML avec schéma de hello et importez-le à la place. Pour plus d’informations sur DSML, consultez [OASIS](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=dsml).

Lorsque vous cliquez sur Suivant, hello UserID et les paramètres de configuration de mot de passe sont vérifiées.

### <a name="global-parameters"></a>Paramètres globaux
Sur la page de paramètres globaux de hello, configurez le fuseau horaire de hello et l’importation de hello et option de l’opération d’exportation.  
![Paramètres globaux](./media/active-directory-aadconnectsync-connector-domino/globalparameters.png)

Hello **fuseau horaire du serveur Domino** paramètre définit l’emplacement de hello de votre serveur Domino.

Cette option de configuration est requise toosupport **importation différentielle** opérations, car elle permet le service de synchronisation hello déterminer les modifications entre les deux derniers importations hello.

>[!Note]
Démarrage de l’écran Paramètres globaux hello hello mars 2017 mise à jour inclut des base de données de messagerie de l’utilisateur hello hello option toodelete lors de la suppression de l’utilisateur hello.

![Suppression de la boîte aux lettres de l’utilisateur](./media/active-directory-aadconnectsync-connector-domino/AdminP.png)

#### <a name="import-settings-method"></a>Paramètres d’importation, méthode
Hello **effectuer une importation complète par** recense les options suivantes :

* Search
* View (recommandée)

**Recherche** est à l’aide de l’indexation dans Domino, mais il est courant que les index hello ne sont pas mis à jour en temps réel et les données de salutation retournées à partir du serveur de hello ne sont pas toujours correctes. Pour un système avec de nombreuses modifications, cette option ne fonctionne pas très bien et indique de fausses suppressions dans certaines situations. Cependant, **Search** est plus rapide que **View**.

**Vue** est hello option recommandée, car il fournit l’état correct de hello de données. Elle est légèrement plus lente que Search.

#### <a name="creation-of-virtual-contact-objects"></a>Création d’objets contact virtuels
Hello **permettre la création de \_objet Contact** recense les options suivantes :

* Aucun
* Non-Reference Values
* Reference and Non-Reference Values

Domino, attributs de référence peuvent contenir plusieurs formats différents tooreference autres objets. toobe toorepresent en mesure de variantes, hello implémente de connecteur \_contacter les objets, également appelé **virtuel Contacts** (VC). Ces objets sont créés afin de pouvoir se joindre à des objets de tooexisting MV ou projetés en tant que de nouveaux objets. Ce qui permet de conserver les références d’attribut.

En activant ce paramètre et si le contenu d’un attribut de référence hello n’est pas un format de nom unique, un \_objet de Contact est créé. Par exemple, un attribut de membre d’un groupe peut contenir des adresses SMTP. Il est également possible de toohave shortName et autres attributs présents dans les attributs de référence. Pour ce scénario, sélectionnez **Non-Reference Values**. Cette configuration est le paramètre le plus courant pour les implémentations de Domino hello.

Une fois Lotus Domino carnets d’adresses distincts de toohave configuré avec des noms différents uniques représentant hello même objet, ses tooalso possible de créer \_objets de Contact pour toutes les valeurs de référence qui sont trouvent dans un carnet d’adresses. Pour ce scénario, sélectionnez hello **référence et des valeurs Non-référence** option.

Si vous avez plusieurs valeurs dans l’attribut de hello **FullName** dans Domino, puis vous également la création de hello tooenable de Contacts virtuel afin de références peuvent être résolus. Par exemple, cet attribut peut avoir plusieurs valeurs après un mariage ou un divorce. Sélectionnez la case à cocher hello **activer... FullName has multiple values** pour ce scénario.

En joignant les attributs appropriés de hello, hello \_objets Contact serait toohello jointes MV objet.

Ces objets ont VC =\_Contact ajouté tootheir DN.

#### <a name="import-settings-conflict-object"></a>Importer les paramètres, objet de conflit
**Exclude Conflict Object**

Dans une implémentation Domino volumineuse, il est possible que plusieurs objets ont hello en raison de problèmes de tooreplication le même nom de domaine. Dans ces cas, le connecteur de hello visualiserez deux objets avec UniversalIDs différents mais le même nom de domaine. Ce conflit provoque un objet temporaire est créé dans l’espace de connecteur hello. Hello connecteur peut ignorer des objets de hello qui ont été sélectionnées dans Domino comme victimes de réplication. recommandation de Hello est tookeep cette case à cocher activée.

#### <a name="export-settings"></a>Paramètres d’exportation
Si hello option **AdminP d’utiliser pour mettre à jour les références** est désactivée, l’exportation d’attributs de référence, tels que des membres, un appel direct et n’utilise pas le processus de AdminP hello. Utilisez uniquement cette option lorsque AdminP n’a pas été configuré toomaintain l’intégrité référentielle.

#### <a name="routing-information"></a>Informations de routage
Dans Domino, il est possible qu’un attribut de référence les informations de routage incorporées sous la forme d’un toohello suffixe DN. Par exemple, attribut de membre hello dans un groupe peut contenir **CN =example/organization@ABC**. suffixe de Hello @ABC est les informations de routage hello. les informations de routage Hello sont utilisées par Domino toosend e-mails toohello correct Domino système, qui peut être un système dans une autre organisation. Dans le champ des informations de routage hello, vous pouvez spécifier utilisés au sein de l’organisation hello dans la portée de hello connecteur de routage des suffixes de hello. Si une de ces valeurs est trouvée en guise de suffixe dans un attribut de référence, les informations de routage hello sont supprimées à partir de la référence de hello. Si le suffixe de routage hello sur une valeur de référence ne peut pas être mise en correspondance tooone de ces valeurs spécifiées, un \_objet de Contact est créé. Ces \_objets Contact sont créés avec **RO = @<RoutingSuffix>**  insérées hello DN. Pour ces \_tooallow rejoindre l’objet réel de tooa si nécessaire les objets de Contact hello suivant des attributs est également ajoutés : \_routingName, \_contactName, \_displayName et UniversalID.

#### <a name="additional-address-books"></a>Carnets d’adresses supplémentaires
Si vous n’avez pas **annuaire** installé, ce qui fournit le nom hello de carnets d’adresses secondaires, puis vous pouvez entrer manuellement ces carnets d’adresses.

#### <a name="multivalued-transformation"></a>Transformation à plusieurs valeurs
Dans Lotus Domino, de nombreux attributs possèdent plusieurs valeurs. Hello des attributs du métaverse correspondant sont généralement unique table. En configurant hello importation et l’option opération d’exportation hello, vous activez toohelp de connecteur hello avec traduction hello requis d’attributs de hello affectée.

**Export**  
option d’opération Hello exportation prend en charge deux modes :

* Append item
* Replace item

**Remplacer l’élément** : lorsque vous sélectionnez cette option, le connecteur hello toujours supprimer hello les valeurs actuelles de l’attribut de hello dans Domino et remplacez par les valeurs hello fourni. Hello fourni table peut être une valeur unique ou à valeurs multiples.

Exemple : attribut de l’Assistant hello d’un objet de la personne a hello valeurs suivantes :

* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Si un nouvel Assistant nommé **David Alexander** est attribuée à toothis personne objet, hello résulte :

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf

**Ajouter l’élément** : lorsque vous sélectionnez cette option, connecteur de hello conserve les valeurs existantes hello sur l’attribut hello Domino et insérer de nouvelles valeurs en haut hello de liste de données hello.

Exemple : attribut de l’Assistant hello d’un objet de la personne a hello valeurs suivantes :

* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Si un nouvel Assistant nommé **David Alexander** est attribuée à toothis personne objet, hello résulte :

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

**Importationation**  
Hello option opération d’importation prend en charge deux modes :

* Default
* Valeur de tooSingle à valeurs multiples

**Par défaut** : lorsque vous sélectionnez l’option par défaut de hello, toutes les valeurs de hello tous les attributs sont importés.

**Valeur de tooSingle à valeurs multiples** : lorsque vous sélectionnez cette option, un attribut à valeurs multiples est converti en un attribut à valeur unique. Si plus d’une valeur existe, valeur hello haut hello (cette valeur est généralement aussi hello plus récentes) est utilisé.

Exemple : attribut de l’Assistant hello d’un objet de la personne a hello valeurs suivantes :

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

Hello dernière mise à jour l’attribut toothis est **David Alexander**. La valeur tooMultivalued tooSingle valeur hello option opération d’importation, le connecteur importe uniquement **David Alexander** dans l’espace connecteur hello.

attributs à valeurs multiples tooconvert logique Hello dans les attributs à valeur unique ne concerne pas les attributs de membre de groupe toohello et toohello personne fullname.

Il également possible tooconfigure importer et exporter des règles de transformation pour les attributs à valeurs multiples par attribut, comme une règle globale toohello d’exception. tooconfigure cette option, entrez [objecttype]. [nom_attribut] Bonjour **importer la liste des attributs d’exclusion** et **exporter la liste d’attributs d’exclusion** zones de texte. Par exemple, si vous entrez Person.Assistant et hello global est défini tooimport toutes les valeurs, seule valeur première hello est importé pour l’assistant hello.

#### <a name="certifiers"></a>Autorités de certification
Toutes les unités d’organisation / d’organisation sont répertoriées par le connecteur de hello. toobe tooexport en mesure de personne objets toohello principal carnet d’adresses, une autorité avec son mot de passe est requise.

Si tous les certificateurs ont hello même mot de passe, hello **mot de passe pour tous les Certifers** peut être utilisé. Vous pouvez entrer le mot de passe hello ici et seul hello autorité fichier spécifié.

Si vous importez uniquement, puis il est inutile toospecify tout certificateurs.

### <a name="configure-provisioning-hierarchy"></a>Configurer la hiérarchie de l’approvisionnement
Lorsque vous configurez le connecteur de Lotus Domino hello, ignorez cette page de boîte de dialogue. connecteur de Lotus Domino Hello ne prend pas en charge la hiérarchie de configuration.  
![Hiérarchie d’approvisionnement](./media/active-directory-aadconnectsync-connector-domino/provisioninghierarchy.png)

### <a name="configure-partitions-and-hierarchies"></a>Configurer des partitions et des hiérarchies
Lorsque vous configurez des partitions et des hiérarchies, vous devez sélectionner le carnet d’adresses principal de hello appelé NAB=names.nsf. En outre toohello principal carnet d’adresses, vous pouvez sélectionner carnets d’adresses secondaires s’ils existent.  
![Partitions](./media/active-directory-aadconnectsync-connector-domino/partitions.png)

### <a name="select-attributes"></a>Sélectionner les attributs
Lorsque vous configurez vos attributs, vous devez sélectionner tous les attributs dont le préfixe est **\_MMS\_**. Ces attributs sont obligatoires lorsque vous configurez de nouveaux objets tooLotus Domino

![Attributs](./media/active-directory-aadconnectsync-connector-domino/attributes.png)

## <a name="object-lifecycle-management"></a>Gestion du cycle de vie des objets
Cette section fournit une vue d’ensemble des différents objets de hello dans Domino.

### <a name="person-objects"></a>Objets Personne
objet de personne Hello représente les utilisateurs de l’organisation et les unités d’organisation. En outre les attributs par défaut de toohello, administrateur de Domino hello peuvent ajouter objet Person de tooa des attributs personnalisés. Au minimum, un objet Personne doit inclure tous les attributs obligatoires. Pour obtenir une liste complète des attributs obligatoires, consultez [Propriétés Lotus Notes](#lotus-notes-properties). tooregister un objet person, hello suivant les conditions préalables doit être remplie :

* Carnet d’adresses Hello (names.nsf) doit avoir été définie, et il doit être le carnet d’adresses principal hello.
* Vous devez disposer un utilisateur particulier hello O/unité d’organisation autorité hello Id et le mot de passe tooregister Bonjour organisation / unité d’organisation.
* Vous devez définir un ensemble spécifique de propriétés Lotus Notes pour un objet Personne. Ces propriétés sont utilisées pour la configuration d’objet de personne hello. Pour plus d’informations, consultez la section hello appelée [propriétés Lotus Notes](#lotus-notes-properties) plus loin dans ce document.
* Hello HTTP mot de passe initial d’une personne est un attribut et un jeu lors de la configuration.
* objet de personne Hello doit être de hello trois types pris en charge suivants :
  1. Normal User, avec un fichier de courrier et un fichier UserID
  2. Roaming User (un Normal User qui inclut tous les fichiers de base de données de l’itinérance)
  3. Contacts (utilisateur sans fichier d’ID)

(À l’exception des contacts) peut plus être regroupées en nous utilisateurs et International tel que défini par la valeur hello hello \_MMS\_IDRegType propriété. Ces personnes utilisent hello Client Notes tooaccess serveurs Lotus Domino, un Id de Notes, et un document de la personne. Si elles utilisent la messagerie Notes, elles ont également un fichier de messagerie. utilisateur de Hello doit être inscrit toobecome active. Pour plus d'informations, consultez les pages suivantes :

* [Configuration d’utilisateurs Notes](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_SETTING_UP_NOTES_USERS.html)
* [Enregistrement des utilisateurs](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_REGISTERING_USERS.html)
* [Gestion des utilisateurs](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_USERS_5151.html)
* [Changement du nom des utilisateurs](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_USER_AUTOMATICALLY.html)

Toutes ces opérations sont effectuées dans Lotus Domino et ensuite importées dans le service de synchronisation hello.

### <a name="resources-and-rooms"></a>Ressources et salles
Une ressource est un autre type d’une base de données dans Lotus Domino. Les ressources peuvent être des salles de conférence avec différents types d’équipements comme des projecteurs. Il existe des sous-types de ressources pris en charge par le connecteur de Lotus Domino qui sont définis par l’attribut de Type de ressource hello :

| Type de ressource | Attribut de type de ressource |
| --- | --- |
| Salle |1 |
| Ressource (autre) |2 |
| Réunion en ligne |3 |

Pour toowork de type hello ressource objet, les éléments suivants de hello sont requis :

* Base de données de réservation de ressources doit déjà exister dans hello connecté Domino server
* site de Hello est déjà défini pour hello ressource

base de données de la réservation de ressources Hello contient trois types de documents :

* Profil du site
* Ressource
* Réservation

Pour plus d’informations sur la configuration de base de données de la réservation de ressources, consultez [Configuration base de données de la ressource réservations hello](https://www-01.ibm.com/support/knowledgecenter/SSKTMJ_8.0.1/com.ibm.help.domino.admin.doc/DOC/H_SETTING_UP_THE_RESOURCE_RESERVATIONS_DATABASE.html).

**Création, mise à jour et suppression de ressources**  
Hello opérations Create, Update et Delete sont exécutées par le connecteur de Lotus Domino hello dans la base de données de la réservation de ressources hello. Ressources sont créées sous forme de documents dans Names.nsf (autrement dit, carnet d’adresses principal hello). Pour plus d’informations sur la modification et la suppression de documents Ressource, consultez [Modification et suppression de documents Ressource](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_EDITING_AND_DELETING_RESOURCE_DOCUMENTS.html).

**Opérations d’importation et d’exportation de ressources**  
Hello ressources peut être importé tooand exporté à partir du service de synchronisation hello, comme tout autre type d’objet. Type d’objet hello sélectionnez en tant que ressource lors de la configuration. Pour que l’opération d’exportation réussisse, vous devez disposer d’informations pour le type de ressource, la base de données de conférence et le nom du site.

### <a name="mail-in-databases"></a>Bases courrier en arrivée
Une base de données de messagerie est une base de données est conçue tooreceive envoie des messages électroniques. Il s’agit d’une messagerie Lotus Domino qui n’est pas associée à un compte d’utilisateur Lotus Domino spécifique (elle ne possède pas son propre fichier d’ID et son propre mot de passe). Une Base courrier en arrivée possède un UserID unique (« nom court ») associé et sa propre adresse e-mail.

Si vous avez besoin d’une messagerie distincte, avec sa propre adresse e-mail partageable avec différents utilisateurs (par exemple, group@contoso.com), une base courrier en arrivée est créée. boîte aux lettres de toothis Hello accès est contrôlé via son contrôle liste accès (ACL), qui contient les noms de hello hello des utilisateurs de Notes autorisées boîte aux lettres de tooopen hello.

Pour obtenir la liste des attributs de hello requis, consultez section hello [attributs obligatoires](#mandatory-attributes) plus loin dans cet article.

Lorsqu’une base de données est conçue tooreceive un message électronique, un document de la messagerie de base de données est créé dans Lotus Domino. Ce document doit exister dans l’annuaire Domino de chaque serveur qui stocke une copie de base de données hello. Pour une description détaillée de la création d’un document Base courrier en arrivée, consultez [Création d’un document Base courrier en arrivée](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_A_MAILIN_DATABASE_DOCUMENT_FOR_A_NEW_DATABASE_OVERVIEW.html).

Avant de créer une base de données de messagerie, base de données hello doit déjà exister (doit ont été créés par l’administrateur de Lotus) sur le serveur de Domino hello.

### <a name="group-management"></a>Gestion des groupes
Vous pouvez obtenir une présentation détaillée de la gestion de groupe hello Lotus Domino depuis hello suivant des ressources :

* [Utilisation de groupes](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_USING_GROUPS_OVER.html)
* [Création d’un groupe](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS_MIDTOPIC_55038956829238418.html)
* [Création et modification de groupes](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS.html)
* [Gestion de groupes](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_GROUPS_1804.html)
* [Renommer un groupe](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_GROUP_STEPS.html)

### <a name="password-management"></a>Gestion des mots de passe
Pour un utilisateur Lotus Domino inscrit, il existe deux types de mots de passe :

1. Mot de passe utilisateur (stocké dans un fichier User.id)
2. Mot de passe Internet / HTTP

connecteur de Lotus Domino Hello prend en charge uniquement les opérations avec le mot de passe HTTP.

gestion des mots de passe tooperform, vous devez activer gestion des mots de passe pour le connecteur hello Bonjour Concepteur de l’Agent de gestion. gestion des mots de passe tooenable, sélectionnez **activer la gestion de mot de passe** sur hello **configurer des Extensions** page de boîte de dialogue.  
![Configure Extensions](./media/active-directory-aadconnectsync-connector-domino/configureextensions.png)

Hello Lotus Domino connecteur prise en charge les opérations de mot de passe Internet suivantes :

* Mot de passe : Mot de passe de définit un nouveau mot de passe Internet/HTTP sur utilisateur hello dans Domino. Par défaut hello compte est également déverrouillé. Hello déverrouiller l’indicateur est exposée sur l’interface WMI hello Hello moteur de synchronisation.
* Modification de mot de passe : Dans ce scénario, un utilisateur un mot de passe toochange hello ou votre est toochange demandées par invite de mot de passe après un certain temps. Pour cet emplacement de tootake opération, à la fois (hello ancien et nouveau mot de passe hello) sont obligatoires. Une fois modifiées, nouveau mot de passe hello est mise à jour dans Lotus Domino.

Pour plus d'informations, consultez les pages suivantes :

* [À l’aide de la fonctionnalité de verrouillage hello Internet](http://www.ibm.com/developerworks/lotus/library/domino8-lockout/)
* [Gestion des mots de passe Internet](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_NOTES_AND_INTERNET_PASSWORD_SYNCHRONIZATION_7570_OVER.html)

## <a name="reference-information"></a>Informations de référence
Cette section répertorie tels que des descriptions d’attribut et les exigences des attributs pour le connecteur de Lotus Domino hello.

### <a name="lotus-notes-properties"></a>Propriétés Lotus Notes
Lorsque vous configurez le répertoire de Lotus Domino Person objets tooyour, vos objets doivent avoir un ensemble spécifique de propriétés avec remplie des valeurs spécifiques. Ces valeurs sont uniquement requises pour les opérations de création.

Hello tableau suivant répertorie ces propriétés et fournit leur description.

| Propriété | Description |
| --- | --- |
| \_MMS_AltFullName |Hello autre complet nom d’utilisateur. |
| \_MMS_AltFullNameLanguage |Hello toobe de langue utilisée pour spécifier le nom complet de hello remplacement de l’utilisateur. |
| \_MMS_CertDaysToExpire |Hello nombre de jours entre hello date actuelle avant de certificat de hello expire. Si non spécifié, date de hello par défaut est de 2 ans à partir de hello date actuelle. |
| \_MMS_Certifier |Propriété qui contient le nom de la hiérarchie d’organisation hello d’autorité de hello. Par exemple : OU=Unité d’organisation,O=Organisation,C=Pays. |
| \_MMS_IDPath |Si la propriété de hello est vide, aucun fichier d’identification utilisateur n’est créé localement sur le serveur de synchronisation de hello. Si la propriété de hello contient un nom de fichier, un fichier d’ID utilisateur est créé dans le dossier de madata hello. propriété de Hello peut également contenir un chemin d’accès complet. |
| \_MMS_IDRegType |Les personnes peuvent être classées dans Contacts, US Users et International Users. Hello tableau suivant répertorie les valeurs possibles de hello : <li>0 - Contact</li><li>1 - Utilisateur des États-Unis</li><li>2 - Utilisateur international</li> |
| \_MMS_IDStoreType |Propriété requise pour US Users et International Users. propriété de Hello contient une valeur entière qui spécifie si l’identification de l’utilisateur hello est stockée en tant que pièce jointe dans le carnet d’adresses Notes hello ou dans le fichier de messagerie de la personne hello. Si le fichier de code utilisateur hello est une pièce jointe dans le carnet d’adresses hello, il peut éventuellement être créé en tant que fichier avec \_MMS_IDPath. <li>Vide : fichier d’ID stocké dans le coffre d’ID, aucun fichier d’identification (utilisé pour les contacts).</li><li> 1 - pièce jointe dans le carnet d’adresses Notes hello. Hello \_MMS_Password propriété doit être définie pour les fichiers d’identification utilisateur qui sont des pièces jointes</li><li>2 : ID stocké dans le fichier de courrier de l’objet Personne. Hello \_MMS_UseAdminP doit être définie de messagerie de hello toofalse toolet fichier est créé au cours de hello d’enregistrement de personne. Hello \_MMS_Password propriété doit être définie pour les fichiers d’identification utilisateur.</li> |
| \_MMS_MailQuotaSizeLimit |nombre de Hello de mégaoctets qui sont autorisés pour la base de données du fichier hello par courrier électronique. |
| \_MMS_MailQuotaWarningThreshold |nombre de Hello de mégaoctets qui sont autorisés pour la base de données de fichier de courrier électronique hello avant un avertissement est émis. |
| \_MMS_MailTemplateName |fichier de modèle du message électronique Hello qui est le fichier de message électronique de l’utilisateur utilisées toocreate hello. Si un modèle est spécifié, fichier de courrier hello est créé à l’aide du modèle spécifié de hello. Aucun modèle n’est spécifié, fichier de modèle par défaut hello est utilisées toocreate hello. |
| \_MMS_OU |Propriété facultative qui est le nom d’unité d’organisation hello sous autorité de hello. Cette propriété doit être vide pour les contacts. |
| \_MMS_Password |Propriété requise pour les utilisateurs. propriété de Hello contient un mot de passe hello pour le fichier d’identification hello d’objet de hello. |
| \_MMS_UseAdminP |Propriété doit être ensemble tootrue si fichier de courrier hello doit être créé par processus de AdminP hello sur serveur Domino de hello (processus d’exportation toohello asynchrone). Si la propriété a la valeur toofalse, fichier de courrier hello est créé avec hello utilisateur Domino (synchrone dans le processus d’exportation hello). |

Pour un utilisateur avec un fichier d’identification associé, hello \_MMS_Password propriété doit contenir une valeur. Pour l’accès à la messagerie via un client de Lotus Notes hello, hello MailServer et MailFile les propriétés d’un utilisateur doivent contenir une valeur.

tooaccess de messagerie via un navigateur Web, hello propriétés suivantes doit contenir des valeurs :

* MailFile - propriété requise qui contient le chemin d’accès de hello sur serveur de Lotus Domino hello où hello messagerie fichier est stocké.
* MailServer - propriété requise qui contient le nom de hello du serveur de Lotus Domino hello. Cette valeur est hello nom toouse lorsque vous avez créé le fichier de courrier Lotus hello sur le serveur de Domino hello.
* HTTPPassword - il s’agit d’une propriété facultative qui contient hello Web mot de passe pour l’objet de hello.

tooaccess hello serveur Domino sans la fonctionnalité de messagerie, hello HTTPPassword propriété doit contenir une valeur. Hello MailFile propriété et hello MailServer propriété peut être vide.

Avec \_MMS_ IDStoreType = 2 (id de magasin dans le fichier de courrier), hello MailSystem, propriété de NotesRegistrationclass a la valeur tooREG_MAILSYSTEM_INOTES (3).

### <a name="mandatory-attributes"></a>Attributs obligatoires
connecteur de Lotus Domino Hello principalement prend en charge que ces types d’objets (types de documents) :

* Groupe
* Base courrier en arrivée
* Personne
* Contact (personne sans autorité de certification)
* Ressource

Cette section répertorie les attributs de hello qui sont obligatoires pour chaque serveur de prise en charge d’objet tooexport tooa Domino.

| Type d'objet | Attributs obligatoires |
| --- | --- |
| Groupe |<li>ListName</li> |
| Base courrier en arrivée |<li>FullName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |
| Personne |<li>LastName</li><li>MailFile</li><li>ShortName</li><li>\_MMS_Password</li><li>\_MMS_IDStoreType</li><li>\_MMS_Certifier</li><li>\_MMS_IDRegType</li><li>\_MMS_UseAdminP</li> |
| Contact (personne sans autorité de certification) |<li>\_MMS_IDRegType</li> |
| Ressource |<li>FullName</li><li>ResourceType</li><li>ConfDB</li><li>ResourceCapacity</li><li>Site</li><li>displayName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |

## <a name="common-issues-and-questions"></a>Questions et problèmes courants
### <a name="schema-detection-does-not-work"></a>La détection du schéma ne fonctionne pas
schéma de toobe toodetect en mesure de hello, il est nécessaire de que ce fichier de schema.nsf hello est présent sur le serveur de Domino hello. Ce fichier s’affiche uniquement si LDAP est installé sur le serveur de hello. Si le schéma de hello n’est pas détectable, vérifiez suivant de hello :

* Hello fichier schema.nsf est présent dans le dossier racine hello Hello serveur Domino
* utilisateur de Hello dispose d’autorisations toosee un fichier schema.nsf hello.
* Forcer un redémarrage du serveur LDAP de hello. Ouvrez **Lotus Domino Console** et utiliser **ReloadSchema de LDAP indiquent** schéma de commande tooreload hello.

### <a name="not-all-secondary-address-books-are-visible"></a>Les carnets d’adresses secondaires ne sont pas tous visibles
Hello Domino connecteur s’appuie sur la fonctionnalité de hello **Directory Assistance** toobe toofind en mesure de hello secondaire carnets. Si la documentation de hello adresse secondaire est manquante, vérifiez si [Directory Assistance](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_DIRECTORY_ASSISTANCE.html) a été activé et configuré sur hello serveur Domino.

### <a name="custom-attributes-in-domino"></a>Attributs personnalisés dans Domino
Il existe plusieurs façons dans le schéma de hello Domino tooextend afin qu’elle apparaisse comme un attribut personnalisé consommable par hello connecteur.

**Approche 1 : Étendre le schéma Lotus Domino**

1. Créer une copie du modèle d’annuaire Domino {PUBNAMES. NTF} en suivant [suit](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (vous devez personnaliser pas de répertoire de IBM Lotus Domino par défaut hello modèle) :
2. Modèle de répertoire de copie de Domino ouvrir hello {CONTOSO. Modèle NTF} qui a été créé dans le Concepteur de Domino et procédez comme suit :
   * Cliquez sur Shared Elements et développez Subforms.
   * Double-cliquez sur sous-formulaire de InheritableSchema ${ObjectName} ({ObjectName} désignant hello nom de classe d’objet structurelle hello par défaut, par exemple : personne).
   * Nom de hello attribut tooadd en schéma {MyPersonAtrribute} et l’attribut toothat correspondant. Créer un champ de par Bonjour sélectionnez **créer** , puis sélectionnez **champ** à partir du menu.
   * Bonjour, ajout du champ, définissez ses propriétés en sélectionnant son Type, taille, le Style, polices et autres paramètres connexes sur la fenêtre des propriétés de champ.
   * Attribut de hello conserver même valeur par défaut en tant que nom hello pour cet attribut (par exemple, si le nom de l’attribut est MyPersonAttribute, conserver la valeur par défaut de hello avec hello même nom).
   * Enregistrer sous-formulaire de hello ${ObjectName} InheritableSchema avec les valeurs mises à jour.
3. Remplacez hello Domino Directory modèle {PUBNAMES. NTF} avec modèle personnalisé nouvelle hello {CONTOSO. NTF} en suivant [suit](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
4. Fermer Domino Admin et ouvrir hello toorestart de Console Domino service LDAP et hello de tooReload schéma LDAP :
   * Dans la Console Domino, insérez commande hello sous **Domino commande** texte classé toorestart le service LDAP hello - [LDAP de tâche redémarrer](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
   * schéma LDAP de tooreload utiliser la commande LDAP de savoir - indiquent les ReloadSchema LDAP
5. Ouvrez Domino Admin et sélectionnez toosee d’onglet utilisateurs et groupes ajoutés attribut est répercutée dans domino ajouter une personne.
6. Ouvrez Schema.nsf dans l’onglet **Files** et vérifiez que l’attribut ajouté figure dans la classe d’objets LDAP dominoPerson.

**Méthode 2 : Créer un auxClass avec l’attribut personnalisé et l’associer à la classe d’objet hello**

1. Créer une copie du modèle d’annuaire Domino {PUBNAMES. NTF} en suivant [suit](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html) (jamais personnaliser du répertoire de IBM Lotus Domino hello par défaut modèle) :
2. Modèle de répertoire de copie de Domino ouvrir hello {CONTOSO. Modèle NTF} a été créé, dans le Concepteur de Domino.
3. Dans le volet gauche de hello, sélectionnez le Code partagé, puis sous-formulaires.
4. Cliquez sur New Subform.
5. Hello toospecify des propriétés de hello sous-formulaire de nouveau hello suivantes :
   * Sous-formulaire de nouveau hello ouvert, choisissez Design - propriétés sous-formulaire
   * Toohello suivant propriété Name, entrez un nom pour la classe d’objet auxiliaire hello--par exemple, TestSubform.
   * Conserver la propriété Options hello « Include dans Insert sous-formulaire... dialogue » sélectionnée
   * Désélectionnez la propriété Options hello « Rendu passent par le code HTML dans les Notes. »
   * Laissez hello autres propriétés même hello et fermer la boîte de propriétés sous-formulaire hello.
   * Enregistrez et fermez sous-formulaire de nouveau hello.
6. Hello suivant tooadd une classe d’objet auxiliaire champ toodefine hello :
   * Ouvrez sous-formulaire hello que vous avez créé.
   * Sélectionnez Create, Field.
   * TooName suivant onglet hello principes fondamentaux de la boîte de dialogue champ hello spécifier n’importe quel nom, par exemple : {MyPersonTestAttribute}.
   * Bonjour, ajout du champ, définissez ses propriétés en sélectionnant son Type, le Style, taille, police et les propriétés associées.
   * Attribut de hello conserver même valeur par défaut en tant que nom hello pour cet attribut (par exemple, si le nom de l’attribut est MyPersonTestAttribute, conserver la valeur par défaut de hello avec hello même nom).
   * Enregistrer les sous-formulaire hello avec les valeurs mises à jour et hello suivant :
     * Dans le volet gauche de hello, sélectionnez le Code partagé, puis sous-formulaires
     * Sélectionnez Nouveau sous-formulaire de hello et choisissez Design - propriétés de la conception.
     * Cliquez sur hello tiers de hello gauche et sélectionnez **propager cette interdiction de modification de conception**.
7. Ouvrez sous-formulaire ExtensibleSchema ${ObjectName} (où {ObjectName} est le nom hello de classe d’objet structurelle hello par défaut, par exemple : personne).
8. Insérer une ressource et sélectionnez hello sous-formulaire (que vous avez créé, par exemple : TestSubform) et enregistrer sous-formulaire de ExtensibleSchema hello ${ObjectName}.
9. Remplacez hello Domino Directory modèle {PUBNAMES. NTF} avec modèle personnalisé nouvelle hello {CONTOSO. NTF} en suivant [suit](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html).
10. Fermer Domino Admin et ouvrir hello toorestart de Console Domino service LDAP et hello de tooReload schéma LDAP :
    * Dans la Console Domino, insérez commande hello sous **Domino commande** texte classé toorestart le service LDAP hello - [LDAP de tâche redémarrer](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html).
    * schéma LDAP tooreload utiliser la commande LDAP de savoir **ReloadSchema de LDAP indiquer**.
11. Ouvrez Domino Admin et sélectionnez toosee d’onglet utilisateurs et groupes ajoutés attribut est répercutée dans domino ajouter une personne (sous d’autres personnes de tabulation).
12. Ouvrez Schema.nsf à partir de l’onglet **Files** et observez l’attribut ajouté sous la classe d’objets auxiliaire TestSubform LDAP.

**Méthode 3 : Ajoutez hello personnalisé toohello ExtensibleObject classe d’attributs**

1. Ouvrir le fichier {Schema.nsf} placé dans le répertoire racine de hello
2. Sélectionnez les Classes d’objet LDAP à partir du menu de gauche hello sous **tous les Documents de schéma** et cliquez sur **classe d’ajouter un objet** bouton :
3. Fournir le nom LDAP hello format {zzzExtensibleSchema} (où zzz est nom hello de classe d’objet structurelle hello par défaut, par exemple personne). Par exemple, schéma de hello tooextend pour la classe d’objet personne, indiquez le nom LDAP {PersonExtensibleSchema}.
4. Fournissez un nom de classe d’objet de qualité supérieure, pour lequel vous souhaitez le schéma de hello tooextend. Par exemple, schéma de hello tooextend classe d’objet personne fournissent le nom de classe supérieur objet {dominoPerson} :
5. Fournir une valide OID correspondant toohello classe d’objet.
6. Sélectionnez les attributs étendus/personnalisé sous les champs obligatoires ou facultatifs des Types d’attributs en fonction de la spécification de hello :
7. Après l’ajout nécessaire d’attributs toohello ExtensibleObjectClass, cliquez sur **Enregistrer & fermer**.
8. Une classe ExtensibleObjectClass est créée pour la classe d’objets par défaut avec des attributs étendus.

## <a name="troubleshooting"></a>Résolution des problèmes
* Pour plus d’informations sur la journalisation de tooenable tootroubleshoot hello connecteur, consultez hello [comment tooEnable le suivi ETW pour les connecteurs](http://go.microsoft.com/fwlink/?LinkId=335731).
