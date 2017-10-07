---
title: "Synchronisation Azure AD Connect : présentation de l’architecture de hello | Documents Microsoft"
description: "Cette rubrique décrit l’architecture de synchronisation Azure AD Connect hello et explique hello termes utilisés."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 465bcbe9-3bdd-4769-a8ca-f8905abf426d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 9fb979fcf8feb7b4d406789102239480b0b4bc94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-architecture"></a>Synchronisation Azure AD Connect : présentation de l’architecture de hello
Cette rubrique décrit l’architecture de base hello pour la synchronisation Azure AD Connect. Dans nombreux aspects, il est similaire tooits prédécesseurs, MIIS 2003, 2007 de ILM et FIM 2010. Synchronisation Azure AD Connect est évolution hello de ces technologies. Si vous êtes familiarisé avec ces technologies antérieures, le contenu de cette rubrique hello sera familier tooyou ainsi. Si vous êtes toosynchronization nouvelle, cette rubrique est pour vous. Il n’est toutefois pas exigence tooknow hello des détails sur cette toobe rubrique réussi à effectuer des personnalisations tooAzure AD Connect synchronisation (moteur de synchronisation appelée dans cette rubrique).

## <a name="architecture"></a>Architecture
moteur de synchronisation Hello crée une vue intégrée des objets qui sont stockées dans plusieurs sources de données connectées et gère les informations d’identité dans ces sources de données. Cet affichage intégré est déterminé par les informations d’identité hello récupérées à partir de sources de données connectées et un ensemble de règles qui déterminent comment tooprocess ces informations.

### <a name="connected-data-sources-and-connectors"></a>Sources de données connectées et connecteurs
moteur de synchronisation Hello traite les informations d’identité à partir de référentiels de données différentes, telles que Active Directory ou d’une base de données SQL Server. Chaque référentiel de données qui organise ses données dans un format de base de données et qui fournit des méthodes d’accès aux données standard est un candidat de source de données potentielles pour le moteur de synchronisation hello. sources de données Hello sont synchronisés par le moteur de synchronisation sont appelés **sources de données connectées** ou **annuaires connectés** (CD).

moteur de synchronisation Hello encapsule l’interaction avec une source de données connectée dans un module appelé un **connecteur**. À chaque type de source de données connectée correspond un connecteur spécifique. Hello connecteur se traduit par une opération requise en format hello hello données connectée source comprend.

Connecteurs effectuer des appels d’API tooexchange informations d’identité (lecture et d’écriture) avec une source de données connectée. Il est également possible de tooadd un connecteur personnalisé à l’aide du framework de connectivité extensible hello. Hello l’illustration suivante montre comment un connecteur connecte à un moteur de synchronisation de données connectée source toohello.

![Arch1](./media/active-directory-aadconnectsync-understanding-architecture/arch1.png)

Les données peuvent circuler dans les deux sens, mais pas simultanément. En d’autres termes, un connecteur peut être configuré tooallow données tooflow à partir du moteur de toosync de source de données connectée hello ou à partir de la source de données connectée du moteur toohello de synchronisation, mais uniquement une de ces opérations peut se produire à tout moment pour un objet et d’attribut. direction de Hello peut être différente pour différents objets et des attributs différents.

tooconfigure un connecteur, vous spécifiez les types d’objets de hello que vous souhaitez toosynchronize. Spécification des types d’objet hello définit étendue hello d’objets qui sont inclus dans le processus de synchronisation hello. étape suivante de Hello est tooselect hello attributs toosynchronize, qui est connue comme une liste d’inclusion d’attributs. Ces paramètres peuvent être modifiés à tout moment dans les règles d’entreprise tooyour toochanges réponse. Lorsque vous utilisez Assistant d’installation Bonjour Azure AD Connect, ces paramètres sont configurés pour vous.

source de données connectée tooexport objets tooa, liste d’inclusion attribut hello doit inclure au moins hello minimale des attributs requis toocreate un objet spécifique de type dans une source de données connectée. Par exemple, hello **sAMAccountName** attribut doit être inclus dans tooexport de liste d’inclusion hello attribut un utilisateur de l’objet tooActive active, car tous les objets utilisateur dans Active Directory doivent avoir un **sAMAccountName**  attribut défini. Là encore, l’Assistant installation hello effectue cette configuration pour vous.

Si la source de données connectée hello utilise des composants structurels, tels que les objets tooorganize partitions ou des conteneurs, vous pouvez limiter les zones hello dans la source de données connectée hello qui sont utilisées pour une solution donnée.

### <a name="internal-structure-of-hello-sync-engine-namespace"></a>Structure interne de l’espace de noms du moteur de synchronisation hello
espace de noms du moteur de synchronisation entier Hello se compose de deux espaces de noms qui stockent des informations d’identité hello. Hello deux espaces de noms sont :

* espace de connecteur Hello (CS)
* Hello métaverse (MV)

Hello **espace connecteur** est une zone de transit qui contient les représentations sous forme de hello désigné des objets à partir d’un attributs hello et de la source de données connectée spécifié dans la liste d’inclusion attribut hello. moteur de synchronisation Hello utilise toodetermine d’espace connecteur hello Nouveautés hello connecté données source et toostage les modifications entrantes. moteur de synchronisation Hello utilise également toostage d’espace connecteur hello sortant des modifications pour la source de données connectée toohello exportation. moteur de synchronisation Hello gère un espace de connecteur distinct comme une zone de transit pour chaque connecteur.

En utilisant une zone de transit, moteur de synchronisation hello reste indépendante des sources de données hello connecté et n’est pas affectée par leur disponibilité et leur accessibilité. Par conséquent, vous pouvez traiter les informations d’identité à tout moment à l’aide des données de salutation dans la zone de transit hello. moteur de synchronisation Hello peut demander uniquement les modifications hello apportées à l’intérieur de source de données connectée hello depuis hello dernière session de communication arrêtée ou par émission de données uniquement hello modifications tooidentity d’informations qui hello de source de données connectée n’a pas encore reçu, ce qui réduit trafic réseau Hello entre le moteur de synchronisation hello et la source de données connectée hello.

En outre, le moteur de synchronisation stocke les informations d’état sur tous les objets qu’il effectue une copie intermédiaire dans l’espace de connecteur hello. Lors de la réception de nouvelles données, le moteur de synchronisation évalue toujours si les données de salutation a déjà été synchronisées.

Hello **métaverse** est une zone de stockage qui contient des informations d’identité hello agrégée à partir de plusieurs sources de données connectées, fournissant une vue globale et intégrée unique de tous les objets combinés. Objets du métaverse sont créés en fonction des informations d’identité hello hello connecté des sources de données et un ensemble de règles qui permettent de processus de synchronisation toocustomize hello sont récupérée.

Hello l’illustration suivante espaces de noms d’espace de connecteur hello et hello métaverse dans le moteur de synchronisation hello.

![Arch2](./media/active-directory-aadconnectsync-understanding-architecture/arch2.png)

## <a name="sync-engine-identity-objects"></a>Objets d’identité du moteur de synchronisation
objets Hello dans le moteur de synchronisation hello sont des représentations sous forme de deux objets de source de données connectée hello ou hello affichage intégré qui le moteur de synchronisation a de ces objets. Chaque objet du moteur de synchronisation doit avoir un GUID. Les GUID garantissent l’intégrité des données et expriment les relations entre les objets.

### <a name="connector-space-objects"></a>Objets de l’espace connecteur
Lorsque le moteur de synchronisation communique avec une source de données connectée, il lit les informations d’identité hello dans la source de données connectée hello et utilise ce toocreate informations une représentation d’objet d’identité hello dans l’espace de connecteur hello. Il est impossible de créer ou de supprimer ces objets individuellement. Cependant, vous pouvez supprimer manuellement tous les objets dans un espace connecteur.

Tous les objets dans l’espace de connecteur hello ont deux attributs :

* Un GUID
* Un nom unique

Si hello connecté source de données assigne un objet de toohello d’attribut unique, puis les objets dans l’espace de connecteur hello peuvent avoir également un attribut d’ancrage. attribut d’ancrage Hello identifie de façon unique un objet dans la source de données connectée hello. moteur de synchronisation Hello utilise hello ancre toolocate hello représentation correspondante de cet objet dans la source de données connectée hello. Moteur de synchronisation suppose que ce point d’ancrage hello d’un objet jamais modifications sur la durée de vie hello d’objet de hello.

La plupart des connecteurs de hello utilisent un toogenerate un identificateur unique connu une ancre automatiquement pour chaque objet lors de son importation. Par exemple, hello connecteur Active Directory utilise hello **objectGUID** attribut pour un point d’ancrage. Pour les sources de données connectée qui ne fournissent pas un identificateur unique clairement défini, vous pouvez spécifier la génération d’ancrage dans le cadre de la configuration du connecteur hello.

Dans ce cas, l’ancre de hello est construit à partir d’un ou plusieurs attributs uniques d’un objet de type, ni de les modifications que vous et qui identifie de façon unique identifie l’objet hello dans l’espace de connecteur hello (par exemple, un numéro d’employé ou un ID d’utilisateur).

Un objet d’espace connecteur peut être hello suivantes :

* Un objet intermédiaire
* Un espace réservé

### <a name="staging-objects"></a>Objets intermédiaires
Un objet intermédiaire représente une instance de hello désigné des types d’objets à partir de la source de données connectée hello. En outre toohello GUID et le nom unique de hello, un objet de zone de transit a toujours une valeur qui indique le type d’objet hello.

Les objets de mise en lots qui ont été importés de toujours ont une valeur pour l’attribut d’ancrage hello. Les objets de mise en lots qui ont été récemment configurés par le moteur de synchronisation et de processus en cours de création dans la source de données connectée hello hello n’ont pas de valeur pour l’attribut d’ancrage hello.

Les objets de mise en lots comportent également des valeurs actuelles des attributs de l’entreprise et des informations opérationnelles requises par le processus de synchronisation de synchronisation du moteur tooperform hello. Informations opérationnelles incluent des indicateurs qui indiquent le type hello des mises à jour sont répliquées sur hello objet intermédiaire. Si un objet intermédiaire a reçu de nouvelles informations d’identité à partir de la source de données connectée hello qui n’a pas encore été traitée, l’objet de hello soit marquée comme en **en attente importation**. Si un objet de mise en lots contient les nouvelles informations d’identité n’a pas encore été la source de données connectée toohello exporté, elle est signalée comme **en attente d’exportation**.

Un objet intermédiaire peut être un objet d’importation ou d’exportation. moteur de synchronisation Hello crée un objet d’importation à l’aide des informations sur l’objet reçues à partir de la source de données connectée hello. Lorsque le moteur de synchronisation reçoit des informations sur l’existence de hello d’un nouvel objet qui correspond à l’un des types d’objet hello sélectionnés Bonjour connecteur, il crée un objet d’importation dans l’espace de connecteur hello en tant que représentation d’objet hello dans la source de données connectée hello.

Hello après l’illustration montre un objet d’importation qui représente un objet dans la source de données connectée hello.

![Arch3](./media/active-directory-aadconnectsync-understanding-architecture/arch3.png)

moteur de synchronisation Hello crée un objet de l’exportation à l’aide des informations relatives aux objets dans le métaverse de hello. Exporter des objets sont source de données connectée toohello exporté au cours de la prochaine session de communication de hello. Point de vue de hello du moteur de synchronisation hello, exporter des objets n’existent pas dans la source de données connectée hello encore. Par conséquent, l’attribut d’ancrage hello pour un objet de l’exportation n’est pas disponible. Après avoir reçu les objet hello à partir du moteur de synchronisation, la source de données connectée hello crée une valeur unique pour l’attribut d’ancrage hello d’objet de hello.

Hello l’illustration suivante montre comment un objet de l’exportation est créé à l’aide des informations d’identité dans le métaverse de hello.

![Arch4](./media/active-directory-aadconnectsync-understanding-architecture/arch4.png)

moteur de synchronisation Hello confirme exportation hello d’objet de hello par réimporter objet hello à partir de la source de données connectée hello. Exporter des objets deviennent importer des objets lorsque le moteur de synchronisation les reçoit lors de l’importation suivante de hello à partir de cette source de données connectée.

### <a name="placeholders"></a>Espaces réservés
moteur de synchronisation Hello utilise un espace de noms plat toostore des objets. Toutefois, certaines sources de données connectées, telles qu’Active Directory, utilisent un espace de noms hiérarchique. tootransform des informations à partir d’un espace de noms hiérarchique dans un espace de noms plat, moteur de synchronisation utilise des espaces réservés toopreserve hello de la hiérarchie.

Chaque espace réservé représente un composant (par exemple, une unité d’organisation) d’un nom d’objet hiérarchique qui n’a pas été importé dans le moteur de synchronisation, mais est nom hiérarchique de hello tooconstruct requis. Leur remplissage vides créés par des références dans tooobjects de source de données hello connecté qui ne sont pas intermédiaire objets dans l’espace de connecteur hello.

moteur de synchronisation Hello utilise également des objets toostore référencé des espaces réservés qui n’ont pas encore été importés. Par exemple, si la synchronisation est l’attribut de gestionnaire configuré tooinclude hello pour hello *Abbie Spencer* de l’objet et la valeur reçue hello est un objet qui n’a pas été importé, telles que *CN = Lee Sperry, CN = Users, DC = fabrikam, DC = com*, informations de gestionnaire hello sont stockées en tant qu’espaces réservés dans l’espace de connecteur hello. Si l’objet de gestionnaire hello est ensuite importée, objet d’espace réservé hello est remplacée par hello objet qui représente le Gestionnaire de hello intermédiaire.

### <a name="metaverse-objects"></a>Objets métaverse
Un objet de métaverse contient hello agrégée vue ce moteur de synchronisation a Hello mise en lots d’objets dans l’espace de connecteur hello. Moteur de synchronisation crée les objets du métaverse à l’aide des informations de hello dans Importer des objets. Plusieurs objets d’espace connecteur peuvent être l’objet de métaverse unique tooa lié, mais un objet d’espace de connecteur ne peut pas être toomore lié à un objet de métaverse.

Les objets métaverse ne peuvent pas être créés ou supprimés manuellement. moteur de synchronisation Hello supprime automatiquement les objets du métaverse qui n’ont pas un objet d’espace connecteur lien tooany dans l’espace de connecteur hello.

objets toomap un données connectée source tooa objet type correspondant dans le métaverse de hello, moteur de synchronisation fournit un schéma extensible avec un ensemble prédéfini de types d’objets et attributs associés. Vous pouvez créer des attributs et des types d’objets pour les objets métaverse. Attributs peuvent être à valeur unique ou à valeurs multiples et les types d’attributs hello peuvent être des chaînes, des références, des chiffres et des valeurs booléennes.

### <a name="relationships-between-staging-objects-and-metaverse-objects"></a>Relations entre les objets intermédiaires et les objets métaverse
Dans l’espace de noms du moteur de synchronisation hello, hello les flux de données sont activé par une relation de lien de hello entre les objets intermédiaires et les objets du métaverse. Objet qui est un intermédiaire objet de métaverse tooa liée est appelée un **joint à un objet** (ou **objet connecteur**). Un objet intermédiaire qui n’est pas lié tooa métaverse objet est appelé un **disjoint objet** (ou **les objets déconnecteurs**). joint des termes du contrat de Hello et disjoint sont préféré toonot confondre avec hello connecteurs responsables de l’importation et exportation de données à partir d’un annuaire connecté.

Espaces réservés ne sont jamais objet de métaverse tooa lié

Un objet joint compose d’un objet de mise en lots et de son objet de métaverse unique tooa relation lié. Objets joints sont des valeurs d’attribut toosynchronize utilisé entre un objet d’espace de connecteur et un objet de métaverse.

Lorsqu’un objet intermédiaire devient un objet joint pendant la synchronisation, les attributs peuvent circuler entre hello hello métaverse objets et mise en lots. Le flux d’attributs est bidirectionnel ; il est configuré à l’aide de règles d’attribut d’importation et d’exportation.

Un objet d’espace connecteur unique peut être lié tooonly métaverse un objet. Toutefois, chaque objet de métaverse peut être ainsi que des objets d’espace de connecteur toomultiple lié Bonjour même ou dans des espaces de connecteur différent, comme indiqué dans hello après l’illustration.

![Arch5](./media/active-directory-aadconnectsync-understanding-architecture/arch5.png)

Hello lié à la relation entre hello objet intermédiaire et un objet de métaverse est persistant et peut être supprimé uniquement par les règles que vous spécifiez.

Un objet disjoint est un objet de mise en lots n’est pas lié tooany métaverse objet. attribut Hello valeurs d’un objet disjoint ne sont pas traités les pages dans le métaverse de hello. Bonjour attribut valeurs d’objet correspondant de hello dans la source de données connectée hello ne sont pas mises à jour par le moteur de synchronisation.

À l’aide des objets disjoints, vous pouvez stocker des informations d’identité dans le moteur de synchronisation et les traiter ultérieurement. Conservation d’un objet de mise en lots en tant qu’objet dans l’espace de connecteur hello disjoint présente de nombreux avantages. Étant donné que le système de hello a déjà généré, hello requis plus d’informations sur cet objet, il n’est pas nécessaire toocreate une représentation sous forme de cet objet lors de hello ensuite importer à partir de la source de données connectée hello. De cette manière, le moteur de synchronisation a toujours un instantané complet de la source de données connectée hello, même s’il n’existe aucune source de données connectée toohello connexion actuelle. Les objets disjoint peuvent être convertis en objets joints et vice versa, selon les règles hello que vous spécifiez.

Un objet d’importation est créé en tant qu’objet disjoint. Un objet d’exportation doit être un objet joint. la logique du système Hello applique cette règle et supprime chaque objet de l’exportation qui n’est pas un objet joint.

## <a name="sync-engine-identity-management-process"></a>Processus de gestion des identités du moteur de synchronisation
processus de gestion des identités Hello contrôle comment les informations d’identité sont mise à jour entre les sources de données connectées différents. La gestion des identités s’effectue en trois phases :

* Importation
* Synchronisation
* Exportation

Au cours du processus d’importation hello, moteur de synchronisation évalue les informations d’identité entrante hello à partir d’une source de données connectée. Lorsque des modifications sont détectées, il crée des objets de mise en lots ou des objets de mise en lots existants dans l’espace de connecteur hello pour la synchronisation des mises à jour.

Au cours du processus de synchronisation hello, moteur de synchronisation met à jour hello métaverse tooreflect modifications qui se sont produites dans l’espace de connecteur hello puis met à jour hello connecteur espace tooreflect qui se sont produites dans le métaverse de hello.

Au cours du processus d’exportation hello, moteur de synchronisation exécute un push des modifications qui sont répliquées sur les objets de mise en lots et qui sont signalés en attente d’exportation.

Hello suivant illustration montre où chaque hello processus se produit en tant que flux d’informations d’identité à partir de tooanother de source de données connectée.

![Arch6](./media/active-directory-aadconnectsync-understanding-architecture/arch6.png)

### <a name="import-process"></a>Processus d’importation
Au cours du processus d’importation hello, moteur de synchronisation évalue les mises à jour des informations tooidentity. Moteur de synchronisation compare les informations d’identité hello reçues à partir de la source de données connectée hello avec les informations d’identité hello sur un objet de mise en lots et détermine si hello objet intermédiaire nécessite des mises à jour. S’il s’agit de hello nécessaires tooupdate objet avec les nouvelles données de mise en lots, hello objet intermédiaire est marquée comme en attente importation.

Par l’intermédiaire des objets dans l’espace de connecteur hello avant la synchronisation, le moteur de synchronisation peut traiter uniquement les informations d’identité hello qui a changé. Ce processus fournit hello avantages suivants :

* **Une synchronisation efficace**. Hello traitées pendant la synchronisation des données est réduit au minimum.
* **Une resynchronisation efficace**. Vous pouvez modifier comment moteur de synchronisation traite les informations d’identité sans source de données toohello reconnexion hello synchronisation moteur.
* **Synchronisation de toopreview opportunité**. Vous pouvez afficher un aperçu des tooverify de synchronisation que vos hypothèses sur les processus de gestion des identités hello sont corrects.

Pour chaque objet spécifié dans le connecteur de hello, moteur de synchronisation hello tente d’abord toolocate une représentation d’objet hello dans l’espace de connecteur hello Hello connecteur. Moteur de synchronisation examine tous les objets de mise en lots dans l’espace de connecteur hello et tente de toofind un objet de mise en lots correspondant qui a un attribut d’ancrage correspondant. Si aucun objet intermédiaire existant n’a une correspondance d’ancrage d’attribut, synchroniser le moteur essaie toofind un objet intermédiaire correspondant avec hello même nom est unique.

Lorsque le moteur de synchronisation détecte un objet de mise en lots qui correspond à par un nom unique, mais pas par un point d’ancrage, hello spéciaux comportement suivant se produit :

* Si l’objet hello situé dans l’espace de connecteur hello n’a aucun point d’ancrage, puis de moteur de synchronisation supprime cet objet à partir de l’espace de connecteur hello et marques hello objet de métaverse il est lié tooas **nouveau la configuration sur l’exécution de la synchronisation suivante**. Il crée ensuite hello nouvelle importation d’objet.
* Si l’objet de hello situé dans l’espace de connecteur hello dispose d’une ancre, moteur de synchronisation suppose que cet objet a été renommé ou supprimé dans l’annuaire connecté de hello. Affecter un nom d’unique temporaire, nouveau pour l’objet d’espace connecteur hello afin qu’il peut préparer objet entrant de hello. Hello ancien objet devient alors **temporaire**, en attente de hello connecteur tooimport hello renommer ou suppression tooresolve hello situation.

Si le moteur de synchronisation localise un objet intermédiaire correspondant toohello l’objet spécifié dans hello connecteur, elle détermine quelles modifications tooapply. Par exemple, moteur de synchronisation peut renommer ou supprimer des objets hello dans la source de données connectée hello, ou il peut uniquement mettre à jour les valeurs d’attribut de l’objet hello.

Les objets intermédiaires avec des données mises à jour sont marqués comme étant en attente d’importation. Plusieurs types d’importation en attente sont disponibles. Selon le résultat de hello hello processus d’importation, un objet de mise en lots dans l’espace de connecteur hello a l’une de hello les types d’importation en attente suivants :

* **None**. Aucune tooany de modifications d’attributs hello Hello objet intermédiaire ne sont disponibles. Le moteur de synchronisation ne marque pas ce type d’un indicateur d’attente d’importation.
* **Ajouter**. Hello objet intermédiaire est un nouvel objet d’importation dans l’espace de connecteur hello. Moteur de synchronisation marque ce type en attente d’importation pour un traitement supplémentaire dans le métaverse de hello.
* **Mettre à jour**. Moteur de synchronisation recherche un objet de mise en lots correspondant dans l’espace de connecteur hello et marque ce type comme en attente importation afin que les mises à jour toohello attributs peuvent être traités dans le métaverse de hello. Les mises à jour comprennent la modification des noms d’objets.
* **Supprimer**. Moteur de synchronisation recherche un objet de mise en lots correspondant dans l’espace de connecteur hello et indicateurs de ce type comme en attente importation afin que hello joint à un objet peut être supprimé.
* **Supprimer/Ajouter**. Moteur de synchronisation recherche un objet de mise en lots correspondant dans l’espace de connecteur hello, mais les types d’objets hello ne correspondent pas. Dans ce cas, une modification de type suppression-ajout est préparée. Une suppression-ajouter modification indique le moteur de synchronisation de toohello une resynchronisation complète de cet objet doit se produire, car différents jeux de règles s’appliquent toothis objet lorsque le type d’objet hello change.

En définissant les hello en attente de l’état de l’importation d’un objet de mise en lots, il est possible tooreduce hello considérablement la quantité de données traitées pendant la synchronisation, car vous pouvez ainsi hello système tooprocess uniquement les objets qui ont mis à jour des données.

### <a name="synchronization-process"></a>Processus de synchronisation
La synchronisation consiste en deux processus connexes :

* Synchronisation entrante, lorsque le contenu de hello métaverse hello est mise à jour à l’aide des données de salutation dans l’espace de connecteur hello.
* Synchronisation sortante, lorsque le contenu de l’espace de connecteur hello hello est mise à jour à l’aide des données dans le métaverse de hello.

En utilisant les informations de hello intermédiaires dans l’espace de connecteur hello, hello le processus de synchronisation entrants crée dans hello métaverse hello intégré vue de données hello qui sont stockées dans des sources de données hello connecté. Tous les objets de mise en lots ou uniquement ceux avec une importation en attente des informations sont agrégées en fonction de la configuration des règles de hello.

mises à jour des processus de synchronisation sortante Hello exporter des objets lorsque les objets du métaverse changent.

Synchronisation entrante crée hello intégré vue dans le métaverse hello hello des informations d’identité qui sont reçus à partir de sources de données hello connecté. Moteur de synchronisation peut traiter les informations d’identité à tout moment à l’aide des dernières informations d’identité hello qu’il a à partir de hello connecté source de données.

**Synchronisation entrante**

Synchronisation entrante inclut hello processus :

* **Disposition** (également appelé **Projection** s’il est important toodistinguish ce processus à partir de la mise en service de synchronisation sortante). moteur de synchronisation Hello crée un nouvel objet de métaverse basé sur un objet de mise en lots et les lie. La configuration est une opération de niveau objet.
* **Jointure**. moteur de synchronisation Hello lie un objet métaverse existants d’objet tooan mise en lots. L’opération de jointure s’effectue au niveau de l’objet.
* **Flux d’attributs d’importation**. Moteur de synchronisation met à jour les valeurs d’attribut hello, appelées le flux d’attribut d’objet hello hello métaverse. Le flux de valeur d’attribut d’importation est une opération au niveau de l’attribut, qui nécessite un lien entre un objet intermédiaire et un objet de métaverse.

Disposition est hello seul processus qui crée des objets dans le métaverse de hello. La configuration affecte uniquement les objets d’importation qui correspondent à des objets disjoints. Au cours de la disposition, moteur de synchronisation crée un objet de métaverse qui correspond le type d’objet toohello de l’objet d’importation hello et établit un lien entre les deux objets, créant ainsi un objet joint.

processus de jointure Hello établit également un lien entre les objets d’importation et d’un objet de métaverse. différence Hello de jointure et de disposition est que le processus de jointure hello requiert cet objet d’importation hello sont liés tooan d’objet métaverse existant où le processus d’approvisionnement hello crée un nouvel objet de métaverse.

Moteur de synchronisation essaie toojoin un objet de métaverse importation objet tooa à l’aide des critères spécifiés dans la configuration de règle de synchronisation hello.

Au cours de la fourniture de hello et les processus de jointure, moteur de synchronisation lie un objet de métaverse tooa un objet, ce qui les rend joint. Une fois ces opérations au niveau objet sont terminées, moteur de synchronisation peut mettre à jour les valeurs d’attribut hello d’objet de métaverse associé hello. Ce processus est appelé flux de valeur d’attribut d’importation.

Importation de flux d’attribut se produit sur tous les objets d’importation qui comportent des nouvelles données et objet de métaverse tooa lié.

**Synchronisation sortante**

La synchronisation sortante met à jour les objets d’exportation lorsqu’un objet métaverse est modifié sans être supprimé. objectif de Hello de synchronisation sortante est tooevaluate si les objets de toometaverse de modifications nécessitent des mises à jour les objets de toostaging dans l’espace de connecteur hello. Dans certains cas, hello modifications peuvent nécessiter la mise en lots des objets dans tous les espaces du connecteur être mis à jour. Les objets intermédiaires modifiés sont marqués d’un indicateur d’attente d’exportation, ce qui fait d’eux des objets d’exportation. Ces objets sont envoyées ultérieurement à la source de données connectée toohello pendant le processus d’exportation hello d’exportation.

La synchronisation sortante s’effectue en trois phases :

* **Approvisionnement**
* **Annulation de l’approvisionnement**
* **Flux de valeur d’attribut d’exportation.**

L’approvisionnement et l’annulation de l’approvisionnement sont des opérations de niveau objet. L’annulation de l’approvisionnement est fonction de l’approvisionnement, car ce dernier est le seul à pouvoir l’initier. Annulation de l’approvisionnement est déclenchée lors de la configuration de lien de hello supprime entre un objet de métaverse et un objet de l’exportation.

Mise en service est toujours déclenchée lorsque les modifications sont appliquées tooobjects hello métaverse. Lorsque des modifications sont apportées les objets toometaverse, moteur de synchronisation peut effectuer les tâches suivantes dans le cadre du processus d’approvisionnement de hello de hello :

* Créer des objets joints, où un objet de métaverse est objet d’exportation tooa lié qui vient d’être créé.
* Le changement de nom d’un objet joint.
* La séparation des liens entre un objet métaverse et des objets intermédiaires, créant un objet disjoint.

Si l’approvisionnement requiert toocreate de moteur de synchronisation un nouvel objet de connecteur, hello mise en lots d’objet de métaverse toowhich hello est lié est toujours un objet de l’exportation, car l’objet de hello n’existe pas encore dans la source de données connectée hello.

Si le provisionnement nécessite l’utilisation du moteur de synchronisation toodisjoin un objet joint, création d’un objet disjoint, la mise hors service est déclenchée. Hello mise hors service des processus supprime l’objet de hello.

Au cours de la mise hors service, suppression d’un objet de l’exportation ne supprime pas physiquement les objet hello. objet Hello est marqué comme en **supprimé**, ce qui signifie que cette opération de suppression hello soit préparé sur l’objet de hello.

Exportation de flux d’attribut se produit également pendant le processus de synchronisation sortante hello, comme toohello qui importent des flux d’attribut se produit pendant la synchronisation entrante. Le flux de valeur d’attribut d’exportation se produit uniquement entre les objets métaverse et les objets d’exportation qui sont joints.

### <a name="export-process"></a>Processus d’exportation
Au cours du processus d’exportation hello, moteur de synchronisation examine tous les objets d’exportation qui sont signalés en attente d’exportation dans l’espace de connecteur hello, puis envoie les mises à jour toohello connecté à la source de données.

moteur de synchronisation Hello peut déterminer la réussite de hello d’une exportation, mais il ne peut pas suffisamment de déterminer que le processus de gestion des identités hello est terminée. Objets de la source de données connectée hello peuvent toujours être modifiées par d’autres processus. Étant donné que le moteur de synchronisation n’a pas de source de données connectée toohello connexion permanente, il n’est pas suffisant hypothèses toomake sur les propriétés d’un objet dans la source de données connectée hello basée uniquement sur une notification de réussite de l’exportation hello.

Par exemple, un processus Bonjour source de données connectée a les attributs de l’objet de modifications hello sauvegarder tootheir des valeurs d’origine (autrement dit, source de données connectée hello peut remplacer les valeurs hello immédiatement après les données hello sont envoyées en arrière par le moteur de synchronisation et correctement appliqué dans la source de données connectée hello).

magasins de moteur de synchronisation Hello exporter et importer des informations d’état sur chaque objet de mise en lots. Si les valeurs des attributs de hello sont spécifiés dans la liste d’inclusion hello attribut ont changé depuis la dernière exportation de hello, hello de stockage de l’importation et d’exportation état Active sync moteur tooreact en conséquence. Moteur de synchronisation utilise hello importation processus tooconfirm valeurs d’attribut qui ont été source de données connectée toohello exporté. Une comparaison entre hello importé et exportés plus d’informations, comme indiqué dans hello suivant illustration, permettent de toodetermine de moteur de synchronisation si l’exportation hello a réussi ou si elle doit toobe répétée.

![Arch7](./media/active-directory-aadconnectsync-understanding-architecture/arch7.png)

Par exemple, si le moteur de synchronisation exporte attribut C, qui a la valeur 5, tooa de source de données connectée, elle stocke C = 5 dans sa mémoire de statut d’exportation. Chaque exportation supplémentaires sur cet objet entraîne à nouveau une source de données connectée toohello tentative tooexport C = 5, car le moteur de synchronisation suppose que cette valeur n’a pas été appliqué de façon persistante toohello objet (autrement dit, sauf si une valeur différente a été récemment importée à partir de hello source de données connectée). mémoire d’exportation Hello est désactivée lors de la réception au cours d’une opération d’importation sur l’objet de hello C = 5.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur hello [synchronisation Azure AD Connect](active-directory-aadconnectsync-whatis.md) configuration.

En savoir plus sur l’ [intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).

