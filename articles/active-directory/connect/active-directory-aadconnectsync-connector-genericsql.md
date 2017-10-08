---
title: aaaGeneric connecteur SQL | Documents Microsoft
description: "Cet article décrit comment le connecteur SQL générique de tooconfigure Microsoft."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: fd8ccef3-6605-47ba-9219-e0c74ffc0ec9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2eab8f0894e83ab4738b9f2deb05b03cdc9a9d43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-technical-reference"></a>Référence technique du connecteur SQL générique
Cet article décrit hello connecteur SQL générique. article de Hello s’applique toohello suite de produits :

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * Nécessité d’utiliser le correctif logiciel 4.1.3671.0 ou une version ultérieure [KB3092178](https://support.microsoft.com/kb/3092178).

MIM2016 et FIM2010R2, hello Connector est disponible en téléchargement à partir de hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495).

toosee ce connecteur dans action, consultez hello [pas à pas le connecteur SQL générique](active-directory-aadconnectsync-connector-genericsql-step-by-step.md) l’article.

## <a name="overview-of-hello-generic-sql-connector"></a>Vue d’ensemble de hello connecteur SQL générique
Hello générique connecteur SQL vous permet de service de synchronisation hello toointegrate avec un système de base de données qui offre une connectivité ODBC.  

À partir d’un point de vue global, hello suivant les fonctionnalités est prises en charge par la version actuelle de hello du connecteur de hello :

| Fonctionnalité | Support |
| --- | --- |
| Source de données connectée |Connecteur de Hello est pris en charge avec tous les pilotes ODBC de 64 bits. Il a été testé avec les éléments suivants de hello : <li>Microsoft SQL Server & SQL Azure</li><li>IBM DB2 10.x</li><li>IBM DB2 9.x</li><li>Oracle 10 & 11g</li><li>MySQL 5.x</li> |
| Scénarios |<li>Gestion du cycle de vie des objets</li><li>Gestion des mots de passe</li> |
| Opérations |<li>Importation complète et importation différentielle, importation, exportation</li><li>Pour l’exportation : ajouter, supprimer, mettre à jour et remplacer</li><li>Définition du mot de passe, modification du mot de passe</li> |
| Schéma |<li>Découverte dynamique des objets et des attributs</li> |

### <a name="prerequisites"></a>Composants requis
Avant d’utiliser hello connecteur, vérifiez que vous disposer de hello sur le serveur de synchronisation hello :

* Microsoft .NET 4.5.2 Framework ou version ultérieure
* Pilotes clients ODBC 64 bits

### <a name="permissions-in-connected-data-source"></a>Autorisations dans la source de données connectée
toocreate ou effectuer une des tâches de hello pris en charge dans le connecteur SQL générique, vous devez avoir :

* db_datareader
* db_datawriter

### <a name="ports-and-protocols"></a>Ports et protocoles
Pour hello les ports requis pour toowork de pilote ODBC hello, consultez la documentation du fournisseur de base de données hello.

## <a name="create-a-new-connector"></a>Créer un connecteur
tooCreate un connecteur SQL générique, dans **Service de synchronisation** sélectionnez **Agent de gestion** et **créer**. Sélectionnez hello **SQL générique (Microsoft)** connecteur.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/createconnector.png)

### <a name="connectivity"></a>Connectivité
Hello connecteur utilise un fichier DSN ODBC pour la connectivité. Créer à l’aide des fichiers de source de données hello **des Sources de données ODBC** trouvé dans le menu Démarrer, hello sous **outils d’administration**. Dans l’outil d’administration de hello, créez un **DSN de fichier** afin qu’il peut être fourni toohello connecteur.

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericsql/connectivity.png)

écran de connectivité Hello est tout d’abord hello lorsque vous créez un nouveau connecteur SQL générique. Vous devez tout d’abord hello tooprovide informations suivantes :

* Chemin d’accès de fichier DSN
* Authentification
  * User Name
  * Mot de passe

base de données Hello doit prendre en charge une de ces méthodes d’authentification :

* **L’authentification Windows**: hello l’authentification de base de données utilise d’utilisateur hello tooverify hello Windows informations d’identification. Hello nom/mot de passe spécifié est tooauthenticate utilisé avec la base de données hello. Ce compte a besoin de base de données toohello d’autorisations.
* **L’authentification SQL**: hello l’authentification de base de données utilise hello/mot de passe utilisateur défini une hello connectivité écran tooconnect toohello base de données. Si vous stockez hello utilisateur nom/mot de passe dans le fichier de source de données hello, informations d’identification de hello fournies à l’écran de connectivité hello ont une priorité.
* **L’authentification de base de données SQL Azure**: pour plus d’informations, consultez [connecter tooSQL de base de données en utilisant authentification Azure Active Directory](../../sql-database/sql-database-aad-authentication.md).

**Nom de domaine est le point d’ancrage**: Si vous sélectionnez cette option, hello DN est également utilisé comme attribut d’ancrage hello. Il peut être utilisé pour une implémentation simple mais a également hello après limitation :

* Le connecteur ne prend en charge qu’un seul type d’objet. Par conséquent, toute référence attributs peuvent faire référence uniquement hello même type d’objet.

**Type d’exportation : Remplacer l’objet**: pendant l’exportation, lorsque seulement certains attributs ont changé, avec tous les attributs de l’objet complet hello est exporté et remplace hello objet existant.

### <a name="schema-1-detect-object-types"></a>Schéma 1 (Détecter les types d’objets)
Dans cette page, vous allez tooconfigure comment hello connecteur est continu toofind hello différents types d’objets de base de données hello.

Chaque type d’objet est présenté sous la forme d’une partition et configuré de manière plus approfondie sur **Configurer des partitions et des hiérarchies**.

![schema1a](./media/active-directory-aadconnectsync-connector-genericsql/schema1a.png)

**Méthode de détection de Type de l’objet**: hello connecteur prend en charge ces méthodes de détection de type objet.

* **Valeur fixe**: fournir de liste hello de types d’objet avec une liste séparée par des virgules. Par exemple : `User,Group,Department`.  
  ![schema1b](./media/active-directory-aadconnectsync-connector-genericsql/schema1b.png)
* **Table/vue/Stored Procedure**: fournissez nom hello de hello table/vue/procédure stockée, puis le nom de la colonne hello qui fournit la liste de hello des types d’objets. Si vous utilisez une procédure stockée, puis fournissent également des paramètres pour ce format de hello **[nom] : [Direction] : [valeur]**. Spécifiez chaque paramètre sur une ligne distincte (utilisez Ctrl + Entrée tooget une nouvelle ligne).  
  ![schema1c](./media/active-directory-aadconnectsync-connector-genericsql/schema1c.png)
* **Requête SQL**: cette option vous permet de tooprovide une requête SQL qui retourne une seule colonne avec les types d’objets, par exemple `SELECT [Column Name] FROM TABLENAME`. Hello retourné de colonne doit être de type chaîne (varchar).

### <a name="schema-2-detect-attribute-types"></a>Schéma 2 (Détecter les types d’attribut)
Dans cette page, vous allez tooconfigure hello comment les noms d’attributs et types vont toobe détecté. options de configuration Hello sont répertoriées pour chaque type d’objet détecté sur la page précédente de hello.

![schema2a](./media/active-directory-aadconnectsync-connector-genericsql/schema2a.png)

**Méthode de détection de Type d’attribut**: hello connecteur prend en charge ces méthodes de détection de type attribut avec chaque type d’objet détecté sur l’écran 1 de schéma.

* **Table/vue/Stored Procedure**: fournir nom hello de hello table/vue/procédure stockée qui doit être des noms d’attribut hello toofind utilisé. Si vous utilisez une procédure stockée, puis fournissent également des paramètres pour ce format de hello **[nom] : [Direction] : [valeur]**. Spécifiez chaque paramètre sur une ligne distincte (utilisez Ctrl + Entrée tooget une nouvelle ligne). noms d’attribut toodetect hello dans un attribut à valeurs multiples, fournissent une liste séparée par des virgules des Tables ou vues. Les scénarios à valeurs multiples ne sont pas pris en charge si les tables parent et enfant ont les mêmes noms de colonnes.
* **Requête SQL**: cette option vous permet de tooprovide une requête SQL qui retourne une seule colonne avec des noms d’attribut, par exemple `SELECT [Column Name] FROM TABLENAME`. Hello retourné de colonne doit être de type chaîne (varchar).

### <a name="schema-3-define-anchor-and-dn"></a>Schéma 3 (Définir le point d’ancrage et le nom unique)
Cette page permet de vous tooconfigure d’ancrage et d’attribut de nom unique pour chaque type d’objet détecté. Vous pouvez sélectionner plusieurs attributs toomake hello d’ancrage unique.

![schema3a](./media/active-directory-aadconnectsync-connector-genericsql/schema3a.png)

* Les attributs à valeurs multiples et booléens ne sont pas répertoriés.
* Même attribut ne peut pas utiliser pour le nom unique et d’ancrage, sauf si **DN est le point d’ancrage** est sélectionné sur la page de connectivité hello.
* Si **DN est le point d’ancrage** est sélectionné sur la page de connectivité hello, cette page nécessite le seul attribut hello DN. Cet attribut est également être utilisé en tant qu’attribut d’ancrage hello.

  ![schema3b](./media/active-directory-aadconnectsync-connector-genericsql/schema3b.png)

### <a name="schema-4-define-attribute-type-reference-and-direction"></a>Schéma 4 (définir le type d’attribut, la référence et la direction)
Cette page vous permet de type d’attribut hello tooconfigure, telles que l’entier, binaire, ou valeur booléenne et la direction de chaque attribut. Tous les attributs de la page **schéma 2** sont répertoriés, et notamment des attributs à valeurs multiples.

![schema4a](./media/active-directory-aadconnectsync-connector-genericsql/schema4a.png)

* **Type de données**: types toothose toomap hello attribut type connus par le moteur de synchronisation hello utilisées. par défaut de Hello hello toouse hello SQL schéma même type, mais DateTime et référence ne sont pas facilement détectables. Pour les, vous devez toospecify **DateTime** ou **référence**.
* **Direction**: vous pouvez définir hello attribut direction tooImport, l’exportation ou ImportExport. ImportExport est la valeur par défaut.

![schema4b](./media/active-directory-aadconnectsync-connector-genericsql/schema4b.png)

Remarques :

* Si un type d’attribut n’est pas détectable par hello connecteur, il utilise le type de données chaîne hello.
* **Tables imbriquées** peuvent être considérées comme des tables de base de données à une colonne. Oracle stocke les lignes hello d’une table imbriquée dans aucun ordre particulier. Toutefois, lorsque vous récupérez la table imbriquée de hello dans une variable de PL/SQL, les indices consécutifs commençant à 1 est attribué aux lignes de hello. Qui vous donne de lignes de tooindividual d’accès de type tableau.
* **VARRYS** ne sont pas pris en charge dans le connecteur de hello.

### <a name="schema-5-define-partition-for-reference-attributes"></a>Schéma 5 (Définir la partition pour les attributs de référence)
Sur cette page, pour tous les attributs de référence, vous configurez la partition (le type d’objet) à laquelle un attribut fait référence.

![schema5](./media/active-directory-aadconnectsync-connector-genericsql/schema5.png)

Si vous utilisez **DN est le point d’ancrage**, vous devez utiliser le même type d’objet comme hello une vous faites référence à partir de hello. Vous ne pouvez pas référencer un autre type d’objet.

>[!NOTE]
À compter de la mise à jour de mars 2017 hello il existe désormais une option pour « * » lorsque cette option est choisie, puis tous les types possibles de membres seront importées.

![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/any-option.png)

>[!IMPORTANT]
 À compter de mai 2017 hello « * » aka **toute option** a été modifiée toosupport importer et exporter des flux. Si vous souhaitez toouse cette option votre table ou de vue à valeurs multiples doit avoir un attribut qui contient le type d’objet hello.

![](./media/active-directory-aadconnectsync-connector-genericsql/any-02.png)

 </br> Si « * » est sélectionné puis hello nom de colonne hello avec le type d’objet hello doit également être spécifié.</br> ![](./media/active-directory-aadconnectsync-connector-genericsql/any-03.png)

Après l’importation, vous voyez quelque chose de similaire image toohello ci-dessous :

  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/after-import.png)



### <a name="global-parameters"></a>Paramètres globaux
page des paramètres globaux Hello est utilisé tooconfigure importation différentielle, format de Date/heure et la méthode de mot de passe.

![globalparameters1](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters1.png)



Hello générique connecteur SQL prend en charge les méthodes suivantes pour l’importation de Delta de hello :

* **Déclencheur**: consultez [Génération de vues différentielles à l’aide de déclencheurs](https://technet.microsoft.com/library/cc708665.aspx).
* **Filigrane**: il s’agit d’une approche numérique qui peut être utilisée avec n’importe quelle base de données. requête de filigrane Hello est préremplie selon le fournisseur de base de données hello. Une colonne de filigrane doit être présente sur chaque tableau/vue affichée. Cette colonne doit effectuer le suivi des insertions et mises à jour des tables de toohello en tant qu’et ses dépendants (à valeurs multiples ou enfant) tables. horloges Hello entre le Service de synchronisation et le serveur de base de données hello doivent être synchronisées. Si ce n’est pas le cas, des entrées dans l’importation de delta hello peuvent être omises.  
  Limite :
  * La stratégie de filigrane ne prend pas en charge les objets supprimés.
* **Instantané**: (fonctionne uniquement avec Microsoft SQL Server) [Génération de vues différentielles à l’aide d’instantanés](https://technet.microsoft.com/library/cc720640.aspx)
* **Suivi des modifications**: (fonctionne uniquement avec Microsoft SQL Server) [About Suivi des modifications](https://msdn.microsoft.com/library/bb933875.aspx)  
  Limites :
  * Ancre & attribut DN doivent être la partie de clé primaire de l’objet sélectionné de hello dans la table de hello.
  * La requête SQL n’est pas prise en charge pendant l’importation et l’exportation avec suivi des modifications.

**Paramètres supplémentaires**: spécifiez hello fuseau horaire du serveur de base de données qui indique où se trouve votre serveur de base de données. Cette valeur est utilisée toosupport hello différents formats de date et heure de début des attributs.

Hello connecteur stocke toujours les date et heure de la date au format UTC. toobe les toocorrectly en mesure de convertir des heures et la date de hello, fuseau horaire de hello du serveur de base de données de hello et format hello utilisé doit être spécifié. format de Hello doit être exprimé au format .net.

Lors de l’exportation, chaque attribut de durée de date doit être fourni toohello connecteur dans le format d’heure UTC.

![globalparameters2](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters2.png)

**Configuration du mot de passe**: connecteur de hello fournit des fonctionnalités de synchronisation de mot de passe et prend en charge et modifier le mot de passe.

Hello connecteur propose deux méthodes de synchronisation de mot de passe toosupport :

* **Procédure stockée**: cette méthode nécessite deux procédures stockées toosupport ensemble & mot de passe de modification. Tapez tous les paramètres pour ajouter et modifier l’opération de mot de passe hello dans **SP de mot de passe défini** et **SP de mot de passe modifier** paramètres respectivement comme par exemple ci-dessous.
  ![globalparameters3](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters3.png)
* **Extension de mot de passe**: cette méthode nécessite des DLL d’extension de mot de passe (vous devez tooprovide hello Extension de nom de la DLL qui implémente hello [IMAExtensible2Password](https://msdn.microsoft.com/library/microsoft.metadirectoryservices.imaextensible2password.aspx) interface). Assembly d’extension de mot de passe doit être placé dans le dossier d’extension afin que le connecteur de hello peut charger hello DLL lors de l’exécution.
  ![globalparameters4](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters4.png)

Vous avez également tooenable hello gestion de mot de passe sur hello **configurer l’Extension** page.
![globalparameters5](./media/active-directory-aadconnectsync-connector-genericsql/globalparameters5.png)

### <a name="configure-partitions-and-hierarchies"></a>Configurer des partitions et des hiérarchies
Sur la page de partitions et des hiérarchies hello, sélectionnez tous les types d’objets. Chaque type d’objet est sa propre partition.

![partitions1](./media/active-directory-aadconnectsync-connector-genericsql/partitions1.png)

Vous pouvez également remplacer les valeurs hello définies sur hello **connectivité** ou **paramètres globaux** page.

![partitions2](./media/active-directory-aadconnectsync-connector-genericsql/partitions2.png)

### <a name="configure-anchors"></a>Configuration de points d’ancrage
Cette page est en lecture seule, car le point d’ancrage hello a déjà été défini. Hello attribut d’ancrage sélectionné est toujours ajoutée avec tooensure de type hello objet il reste unique entre les types d’objets.

![Points d’ancrage](./media/active-directory-aadconnectsync-connector-genericsql/anchors.png)

## <a name="configure-run-step-parameter"></a>Configurer le paramètre d’exécution d’étape
Ces étapes sont configurés sur hello sur hello connecteur, les profils d’exécution. Ces configurations hello réelle de l’importation et exportation de données.

### <a name="full-and-delta-import"></a>Importation complète et différentielle
Le connecteur SQL générique prend en charge les importations complètes et différentielles par le biais des méthodes qui suivent :

* Table
* Affichage
* Procédure stockée
* Requête SQL

![runstep1](./media/active-directory-aadconnectsync-connector-genericsql/runstep1.png)

**Table/Vue**  
les attributs à valeurs multiples tooimport pour un objet, vous avez le nom de table ou de vue séparées par des virgules tooprovide hello **vues de la table nom d’à valeurs multiples** et les conditions de jointure respectifs Bonjour **deconditiondejointure**avec la table parente hello.

Exemple : Vous souhaitez objet Employee de hello tooimport et tous ses attributs à valeurs multiples. Il existe deux tables nommées respectivement Employé (table principale) et Service (valeur multiple).
Hello suivant :

* Saisissez **Employé** dans **Table/Vue/Nom unique**.
* Saisissez le service dans **Nom de table/vue à valeurs multiples**.
* Type de condition de jointure hello entre Employee et Department dans **Condition de jointure**, par exemple `Employee.DEPTID=Department.DepartmentID`.
  ![runstep2](./media/active-directory-aadconnectsync-connector-genericsql/runstep2.png)

**Procédures stockées**  
![runstep3](./media/active-directory-aadconnectsync-connector-genericsql/runstep3.png)

* Si vous avez beaucoup de données, il est recommandé de pagination tooimplement avec vos procédures stockées.
* Pour votre pagination toosupport de procédure stockée, vous devez tooprovide Index de début et fin. Voir : [Pagination efficace dans de grandes quantités de données](https://msdn.microsoft.com/library/bb445504.aspx).
* @StartIndex et @EndIndex sont remplacés au moment de l’exécution par la valeur de taille configurée sur la page **Étape de configuration**. Par exemple, lorsque le connecteur de hello récupère première page et taille de la page hello a la valeur 500, dans une telle situation @StartIndex serait 1 et @EndIndex 500. Ces valeurs augmenter lorsque le connecteur récupère les pages suivantes et modifier hello @StartIndex & @EndIndex valeur.
* tooexecute paramétrable de la procédure stockée, fournissez les paramètres hello dans `[Name]:[Direction]:[Value]` format. Entrez chaque paramètre sur une ligne distincte (utilisez Ctrl + Entrée tooget une nouvelle ligne).
* Le connecteur SQL générique prend également en charge l’opération d’importation à partir des serveurs liés dans Microsoft SQL Server. Si les informations doivent être récupérées à partir d’une Table dans un serveur lié, Table doit être fournie au format de hello :`[ServerName].[Database].[Schema].[TableName]`
* Le connecteur SQL générique prend en charge uniquement les objets dont la structure est similaire (les alias et le type de données) entre les informations d’étapes d’exécution et la détection de schéma. Si hello sélectionné l’objet de schéma et les informations fournies à l’étape d’exécution est différent, le connecteur SQL est toosupport Impossible de ce type de scénarios.

**Requête SQL**  
![runstep4](./media/active-directory-aadconnectsync-connector-genericsql/runstep4.png)

![runstep5](./media/active-directory-aadconnectsync-connector-genericsql/runstep5.png)

* Les requêtes à jeux de résultats multiples ne sont pas prises en charge.
* Requête SQL prend en charge la pagination de hello et fournit de départ Index et l’Index de fin comme une pagination toosupport variable.

### <a name="delta-import"></a>Importation d’écart
![runstep6](./media/active-directory-aadconnectsync-connector-genericsql/runstep6.png)

L’importation d’écart requiert une configuration plus importante que l’importation intégrale.

* Si vous choisissez approche de déclencheur ou d’un instantané hello modifications delta de tootrack, puis fournir une Table d’historique ou d’un instantané de base de données dans **nom de base de données de la Table d’historique ou d’un instantané** boîte.
* Vous devez également tooprovide condition de jointure entre la table d’historique et de la table Parent, par exemple`Employee.ID=History.EmployeeID`
* transaction de hello tootrack sur la table parent de hello à partir de la table d’historique hello, vous devez fournir le nom de la colonne hello qui contient des informations d’opération hello (Add/Update/Delete).
* Si vous choisissez de filigrane tootrack modifications delta, puis fournir de nom de la colonne hello qui contient des informations d’opération hello dans **colonne nom de la marque l’eau**.
* Hello **modifier l’attribut de Type** colonne est requise pour modifier le type hello. Cette colonne est mappée à une modification qui se produit dans la table primaire de hello ou tableau de valeurs multiples tooa type dans la vue de delta hello. Cette colonne peut contenir hello Modify_Attribute modifier le type de modifications au niveau de l’attribut ou un ajouter, modifier ou supprimer changer de type pour un type de modifications au niveau de l’objet. Si elle est autre chose qu’une valeur par défaut hello ajouter, modifier ou supprimer, puis vous pouvez définir ces valeurs à l’aide de cette option.

### <a name="export"></a>Exportation
![runstep7](./media/active-directory-aadconnectsync-connector-genericsql/runstep7.png)

Le connecteur SQL générique prend en charge l’exportation en utilisant quatre méthodes prises en charge telles que :

* Table
* Affichage
* Procédure stockée
* Requête SQL

**Table/Vue**  
Si vous choisissez hello option de Table ou de vue, puis le connecteur hello génère hello requêtes respectives toodo hello exportation.

**Procédures stockées**  
![runstep8](./media/active-directory-aadconnectsync-connector-genericsql/runstep8.png)

Si vous choisissez d’option de procédure stockée hello, exportation requiert trois opérations de Insert/Update/Delete stockée procédures tooperform différents.

* **Ajoutez le nom du Service Pack**: ce Service Pack s’exécute si n’importe quel objet vient tooconnector pour l’insertion dans la table correspondante de hello.
* **Mettre à jour le nom du Service Pack**: ce Service Pack s’exécute si n’importe quel objet vient tooconnector pour la mise à jour dans la table correspondante de hello.
* **Supprimer le nom du Service Pack**: ce Service Pack s’exécute si n’importe quel objet vient tooconnector pour la suppression de table respectives de hello.
* Attribut sélectionné à partir du schéma hello utilisé en tant que paramètre valeur toohello stockée procédure. Par exemple, `EmployeeName: INPUT: @EmployeeName` (EmployeeName est sélectionné dans le schéma de connecteur hello et connecteur de hello remplace la valeur correspondante de hello pendant cette opération d’exportation)
* toorun paramétré la procédure stockée, fournir des paramètres dans `[Name]:[Direction]:[Value]` format. Entrez chaque paramètre sur une ligne distincte (utilisez Ctrl + Entrée tooget une nouvelle ligne).

**SQL query**  
![runstep9](./media/active-directory-aadconnectsync-connector-genericsql/runstep9.png)

Si vous choisissez d’option de requête SQL hello, exportation nécessite que trois différentes requêtes tooperform les opérations Insert/Update/Delete.

* **Requête Insert**: cette requête est exécutée si n’importe quel objet vient tooconnector pour l’insertion dans la table correspondante de hello.
* **Mettre à jour de la requête**: cette requête est exécutée si n’importe quel objet vient tooconnector pour la mise à jour dans la table correspondante de hello.
* **Supprimer la requête**: cette requête est exécutée si n’importe quel objet vient tooconnector pour la suppression de table respectives de hello.
* Attribut sélectionné à partir du schéma hello utilisé en tant que paramètre valeur toohello requête, par exemple`Insert into Employee (ID, Name) Values (@ID, @EmployeeName)`

## <a name="troubleshooting"></a>Résolution des problèmes
* Pour plus d’informations sur la journalisation de tooenable tootroubleshoot hello connecteur, consultez hello [comment tooEnable le suivi ETW pour les connecteurs](http://go.microsoft.com/fwlink/?LinkId=335731).
