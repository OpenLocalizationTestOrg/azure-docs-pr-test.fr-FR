---
title: "aaaOverview de contrôle d’accès dans Data Lake Store | Documents Microsoft"
description: "Comprendre le fonctionnement du contrôle d’accès dans Azure Data Lake Store"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: d16f8c09-c954-40d3-afab-c86ffa8c353d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 1cc5d578f22ef0a123a1547abebfb4795ea09139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-control-in-azure-data-lake-store"></a>Contrôle d’accès dans Azure Data Lake Store

Azure Data Lake Store implémente un modèle de contrôle d’accès qui dérive de HDFS, qui dérive à son tour de modèle de contrôle d’accès POSIX hello. Cet article résume les principes fondamentaux de hello de modèle de contrôle d’accès hello pour Data Lake Store. toolearn en savoir plus sur le modèle de contrôle d’accès hello HDFS, consultez [HDFS autorisations Guide](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html).

## <a name="access-control-lists-on-files-and-folders"></a>Listes de contrôle d’accès sur les fichiers et dossiers

Il existe deux types de listes de contrôle d’accès (ACL) : les **ACL d’accès** et les **ACL par défaut**.

* **Accès ACL**: ces objets de tooan contrôle l’accès. Les fichiers et les dossiers ont tous des ACL d’accès.

* **ACL par défaut**: un « modèle » des ACL associé à un dossier qui déterminent les listes d’accès hello ACL pour tous les éléments enfants qui sont créés sous ce dossier. Les fichiers n’ont pas d’ACL par défaut.

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-1.png)

Accès ACL et par défaut des ACL ont hello même structure.

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-2.png)



> [!NOTE]
> Modification hello ACL par défaut d’un parent n’affecte pas hello accès ou ACL par défaut des éléments enfants qui existent déjà.
>
>

## <a name="users-and-identities"></a>Utilisateurs et identités

Chaque fichier et dossier dispose d’autorisations distinctes pour ces identités :

* Hello utilisateur du fichier de hello propriétaire
* groupe propriétaire de Hello
* Les utilisateurs nommés
* Les groupes nommés
* Tous les autres utilisateurs

les identités des utilisateurs et groupes Hello sont les identités Azure Active Directory (Azure AD). Ainsi sauf indication contraire, un « utilisateur, » dans le contexte de hello Lake du magasin de données, permettant une signifie un utilisateur Azure AD ou un groupe de sécurité Azure AD.

## <a name="permissions"></a>Autorisations

Hello les autorisations sur un objet de système de fichiers sont **en lecture**, **écrire**, et **Execute**, et ils peuvent être utilisés sur les fichiers et dossiers comme indiqué dans hello tableau suivant :

|            |    Fichier     |   Dossier |
|------------|-------------|----------|
| **Lecture (R)** | Peut lire contenu hello d’un fichier | Requiert **en lecture** et **Execute** contenu de hello toolist du dossier de hello|
| **Écriture (W)** | Écrire ou ajouter le fichier de tooa | Requiert **écrire** et **Execute** toocreate des éléments enfants dans un dossier |
| **Exécution (X)** | Ne signifie pas que n’importe où dans le contexte de hello de Data Lake Store | Éléments requis tootraverse hello enfant d’un dossier |

### <a name="short-forms-for-permissions"></a>Formes abrégées des autorisations

**RWX** est utilisé tooindicate **lecture + écriture + exécuter**. Il existe une forme numérique plus condensée dans lequel **lecture = 4**, **écrire = 2**, et **Execute = 1**, somme hello qui représente les autorisations hello. Voici quelques exemples.

| Forme numérique | Forme abrégée |      Signification     |
|--------------|------------|------------------------|
| 7            | RWX        | Lecture + Écriture + Exécution |
| 5            | R-X        | Lecture + Exécution         |
| 4            | R--        | Lire                   |
| 0            | ---        | | Aucune autorisation         |


### <a name="permissions-do-not-inherit"></a>Les autorisations ne se transmettent pas en héritage

Modèle de style POSIX hello qui est utilisé par Data Lake Store, autorisations pour un élément sont stockées sur élément hello proprement dit. En d’autres termes, les autorisations pour un élément ne peut pas être héritées hello des éléments de parents.

## <a name="common-scenarios-related-toopermissions"></a>Toopermissions connexes des scénarios courants

Voici certaines toohelp de scénarios courants vous comprenez quelles autorisations sont nécessaires tooperform certaines opérations sur un compte Data Lake Store.

### <a name="permissions-needed-tooread-a-file"></a>Autorisations nécessaires tooread un fichier

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-3.png)

* Pour hello toobe de fichier en lecture, hello appelant besoins **en lecture** autorisations.
* Pour tous les hello dans la structure de dossiers hello des dossiers qui contiennent les fichiers hello, hello appelant besoins **Execute** autorisations.

### <a name="permissions-needed-tooappend-tooa-file"></a>Autorisations nécessaires tooappend tooa fichier

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-4.png)

* Pour hello fichier toobe ajoutée, hello appelant besoins **écrire** autorisations.
* Pour tous les hello dossiers qui contiennent les fichiers hello, hello appelant besoins **Execute** autorisations.

### <a name="permissions-needed-toodelete-a-file"></a>Autorisations nécessaires toodelete un fichier

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-5.png)

* Dossier parent de hello, hello appelant besoins **écrire + exécuter** autorisations.
* Pour tous les hello autres dossiers dans le chemin d’accès du fichier hello, hello appelant besoins **Execute** autorisations.



> [!NOTE]
> Écrire des autorisations sur le fichier de hello ne sont pas requis toodelete il tant que hello deux conditions précédentes sont remplies.
>
>

### <a name="permissions-needed-tooenumerate-a-folder"></a>Autorisations nécessaires tooenumerate un dossier

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-6.png)

* Pour hello dossier tooenumerate, hello appelant besoins **lecture + Execute** autorisations.
* Pour tous les hello dossiers de niveau supérieur, les besoins de l’appelant de hello **Execute** autorisations.

## <a name="viewing-permissions-in-hello-azure-portal"></a>Autorisations d’affichage Bonjour portail Azure

À partir de hello **Explorateur de données** Panneau de hello compte Data Lake Store, cliquez sur **accès** toosee hello ACL pour un fichier ou un dossier. Cliquez sur **accès** toosee hello ACL pour hello **catalogue** dossier sous hello **mydatastore** compte.

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-1.png)

Dans ce panneau, section supérieure de hello montre une vue d’ensemble d’autorisations hello dont vous disposez. (Dans la capture d’écran de hello, hello se Bob.) Après cela, les autorisations d’accès hello sont affichées. Après cela, à partir de hello **accès** panneau, cliquez sur **vue Simple** toosee hello vue plus simple.

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-simple-view.png)

Cliquez sur **vue avancée** toosee hello plus vue avancée, où les concepts hello de super utilisateur, le masque et par défaut des ACL sont affichés.

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-advance-view.png)

## <a name="hello-super-user"></a>super utilisateur de Hello

Un super utilisateur a hello la plupart des droits de tous les utilisateurs de hello Bonjour Data Lake Store. Un super utilisateur :

* A les autorisations RWX trop**tous les** fichiers et dossiers.
* Peut modifier les autorisations de hello sur n’importe quel fichier ou un dossier.
* Peut modifier hello utilisateur propriétaire ou le propriétaire de groupe de tout fichier ou dossier.

Dans Azure, un compte Data Lake Store possède plusieurs rôles Azure :

* Propriétaires
* Contributeurs
* Lecteurs

Tout le monde Bonjour **propriétaires** rôle pour un compte Data Lake Store est automatiquement un super utilisateur pour ce compte. toolearn, voir [contrôle d’accès basé sur le rôle](../active-directory/role-based-access-control-configure.md).
Si vous voulez toocreate un rôle personnalisé contrôle d’accès en fonction du rôle (RBAC) qui dispose des autorisations de super utilisateur, il doit hello toohave les autorisations suivantes :
- Microsoft.DataLakeStore/accounts/Superuser/action
- Microsoft.Authorization/roleAssignments/write


## <a name="hello-owning-user"></a>utilisateur propriétaire de Hello

Hello utilisateur qui a créé l’élément de hello est automatiquement hello utilisateur de l’élément de hello propriétaire. Les utilisateurs propriétaires peuvent :

* Modifier les autorisations de hello d’un fichier qui est la propriété.
* Modifier hello propriétaire de groupe d’un fichier qui appartient, tant que l’utilisateur propriétaire de hello est également un membre du groupe cible de hello.

> [!NOTE]
> Hello utilisateur propriétaire *ne peut pas* modifier hello utilisateur du fichier appartenant à un autre propriétaire. Seuls les super utilisateurs peuvent modifier hello propriétaire l’utilisateur d’un fichier ou un dossier.
>
>

## <a name="hello-owning-group"></a>groupe propriétaire de Hello

Bonjour POSIX ACL, chaque utilisateur est associé à un « groupe principal ». Par exemple, l’utilisateur « alice » peut appartenir au groupe « finance » toohello. Alice peut également appartenir toomultiple groupes, mais un seul groupe est toujours désigné comme son groupe principal. Dans POSIX, lorsqu’Alice crée un fichier, hello propriétaire de groupe de ce fichier a la valeur tooher groupe principal, qui dans ce cas est « Finances ».

Lorsqu’un nouvel élément de système de fichiers est créé, Data Lake Store assigne un toohello valeur groupe propriétaire.

* **Cas n° 1**: dossier racine de hello « / ». Ce dossier est créé lors de la création d’un compte Data Lake Store. Dans ce cas, le groupe propriétaire de hello est définie utilisateur toohello qui a créé le compte de hello.
* **Cas n° 2** (tous les autres cas) : lorsqu’un nouvel élément est créé, le groupe propriétaire de hello est copié à partir du dossier parent hello.

groupe propriétaire de Hello peut être modifié par :
* un super utilisateur ;
* Hello propriétaire l’utilisateur, si l’utilisateur propriétaire de hello est également un membre du groupe cible de hello.

## <a name="access-check-algorithm"></a>Algorithme de vérification des accès

Hello suivant illustration représente l’algorithme de vérification d’accès hello pour les comptes Data Lake Store.

![Algorithme d’ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-algorithm.png)


## <a name="hello-mask-and-effective-permissions"></a>masque de Hello et « autorisations effectives »

Hello **masque** est un RWX valeur accès toolimit utilisés pour **des utilisateurs nommés**, hello **groupe propriétaire**, et **groupes nommés** lorsque vous êtes exécution d’algorithme de vérification d’accès hello. Vous trouverez ici les concepts clés de hello pour le masque de hello.

* masque de Hello crée « autorisations effectives ». Autrement dit, il modifie les autorisations de hello au moment de hello de vérification d’accès.
* masque de Hello peut être modifié directement par le propriétaire du fichier hello et tous les super utilisateurs.
* masque de Hello peut supprimer l’autorisation effective d’autorisations toocreate hello. masque de Hello *ne peut pas* ajouter l’autorisation effective de toohello autorisations.

Prenons quelques exemples. Dans l’exemple suivant de hello, masque de hello est défini trop**RWX**, ce qui signifie que le masque hello ne supprime pas les autorisations. les autorisations effectives Hello pour hello nommé utilisateur, le groupe propriétaire et groupe nommé ne sont pas modifiées au cours de la vérification d’accès hello.

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-1.png)

Dans l’exemple suivant de hello, masque de hello est défini trop**R-X**. Cela signifie qu’il **désactive les autorisations d’écriture hello** pour **utilisateur nommé**, **groupe propriétaire**, et **groupe nommé** au moment de hello d’accès vérification.

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-mask-2.png)

Pour référence, voici où masque hello pour un fichier ou un dossier s’affiche dans hello portail Azure.

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-show-acls-mask-view.png)

> [!NOTE]
> Un nouveau compte Data Lake Store, hello et masque de pour hello accès ACL par défaut de la racine de hello dossier (« / ») par défaut est tooRWX.
>
>

## <a name="permissions-on-new-files-and-folders"></a>Autorisations sur les nouveaux fichiers et dossiers

Lorsqu’un nouveau fichier ou dossier est créé dans un dossier existant, hello ACL par défaut sur le dossier parent de hello détermine :

- L’ACL par défaut et l’ACL d’accès d’un dossier enfant
- L’ACL d’accès d’un fichier enfant (les fichiers n’ont pas d’ACL par défaut)

### <a name="hello-access-acl-of-a-child-file-or-folder"></a>Hello d’accès d’un fichier enfant ou un dossier

Lorsqu’un fichier enfant ou un dossier est créé, ACL par défaut de hello parent est copié en tant que hello d’accès du fichier d’enfant hello ou du dossier. En outre, si **autres** utilisateur dispose d’autorisations de RWX dans l’ACL par défaut du parent hello, il est supprimé d’accès l’élément enfant de hello.

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-1.png)

Dans la plupart des scénarios, les informations précédentes hello sont tous les tooknow sur la manière dont l’accès d’un élément enfant est déterminé. Toutefois, si vous êtes familiarisé avec les systèmes POSIX et que vous souhaitez toounderstand détaillée la réalisation de cette transformation, consultez la section de hello [rôle du Umask lors de la création de hello accès pour les nouveaux fichiers et dossiers](#umasks-role-in-creating-the-access-acl-for-new-files-and-folders) plus loin dans cet article.


### <a name="a-child-folders-default-acl"></a>ACL par défaut pour un dossier enfant

Création d’un dossier enfant sous un dossier parent, par défaut de liste ACL du dossier hello parent est copiée via comme l’ACL du dossier toohello enfant par défaut est.

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-child-items-2.png)

## <a name="advanced-topics-for-understanding-acls-in-data-lake-store"></a>Rubriques avancées permettant de comprendre les ACL dans Data Lake Store

Voici certains toohelp rubriques avancées que vous comprenez comment les ACL sont déterminées pour Data Lake Store fichiers ou dossiers.

### <a name="umasks-role-in-creating-hello-access-acl-for-new-files-and-folders"></a>Rôle du umask lors de la création de hello accès pour les nouveaux fichiers et dossiers

Dans un système compatible POSIX, concept général de hello est qu’umask est une valeur de bit 9 sur le dossier parent hello qui a utilisé l’autorisation de hello tootransform pour **utilisateur propriétaire**, **groupe propriétaire**, et  **autres** sur hello accès d’un nouveau fichier enfant ou un dossier. bits Hello d’un umask identifient quels tooturn bits hors tension dans accès l’élément enfant de hello. Par conséquent, il est utilisé tooselectively empêcher la propagation des autorisations pour hello **utilisateur propriétaire**, **groupe propriétaire**, et **autres**.

Dans un système HDFS, hello umask est généralement une option de configuration au niveau du site qui est contrôlée par les administrateurs. Data Lake Store utilise un **umask à l’échelle du compte** qui ne peut pas être modifié. Hello suivant table affiche hello Démasquez à Data Lake Store.

| Groupe d'utilisateurs  | Paramètre | Effet sur l’ACL d’accès du nouvel élément enfant |
|------------ |---------|---------------------------------------|
| utilisateur propriétaire | ---     | Aucun effet                             |
| groupe propriétaire| ---     | Aucun effet                             |
| autre       | RWX     | Supprimer les autorisations Lecture + Écriture + Exécution         |

Hello après l’illustration montre cette umask en action. effet net de Hello est tooremove **lecture + écriture + exécuter** pour **autres** utilisateur. Étant donné que hello umask n’a pas spécifié de bits pour **utilisateur propriétaire** et **groupe propriétaire**, ces autorisations ne sont pas transformées.

![ACL Data Lake Store](./media/data-lake-store-access-control/data-lake-store-acls-umask.png)

### <a name="hello-sticky-bit"></a>bit de pense-bête Hello

bit de pense-bête Hello est une fonctionnalité plus avancée d’un système de fichiers POSIX. Dans le contexte de hello Lake du magasin de données, il est peu probable que le bit rémanentes hello est nécessaire.

Hello tableau suivant présente le fonctionnement des bits de pense-bête hello dans Data Lake Store.

| Groupe d'utilisateurs         | Fichier    | Dossier |
|--------------------|---------|-------------------------|
| Sticky bit **DÉSACTIVÉ** | Aucun effet   | Aucun effet           |
| Sticky bit **ACTIVÉ**  | Aucun effet   | Empêche une personne d’autre que **super utilisateurs** et hello **utilisateur propriétaire** d’un élément enfant à partir de la supprimer ou renommer cet élément enfant.               |

bit de pense-bête Hello n’est pas affiché dans hello portail Azure.

## <a name="common-questions-about-acls-in-data-lake-store"></a>Questions les plus fréquentes sur les ACL dans Data Lake Store

Voici quelques questions fréquentes concernant les ACL dans Data Lake Store.

### <a name="do-i-have-tooenable-support-for-acls"></a>Prise en charge de tooenable des ACL ai-je besoin ?

Non. Le contrôle d’accès via les ACL est toujours activé pour les comptes Data Lake Store.

### <a name="which-permissions-are-required-toorecursively-delete-a-folder-and-its-contents"></a>Les autorisations qui sont requis toorecursively les supprimer un dossier et son contenu ?

* le dossier parent Hello doit avoir **écrire + exécuter** autorisations.
* Hello toobe dossier supprimé et tous les dossiers qu’il contient, nécessite **lecture + écriture + exécuter** autorisations.

> [!NOTE]
> Il est inutile d’autorisations d’écriture toodelete fichiers dans des dossiers. En outre, hello du dossier racine « / » peut **jamais** être supprimé.
>
>

### <a name="who-is-hello-owner-of-a-file-or-folder"></a>Qui est propriétaire de hello d’un fichier ou un dossier ?

créateur de Hello d’un fichier ou dossier devient propriétaire de hello.

### <a name="which-group-is-set-as-hello-owning-group-of-a-file-or-folder-at-creation"></a>Le groupe est défini comme propriétaire de groupe d’un fichier ou dossier lors de la création de hello ?

groupe propriétaire de Hello est copié à partir de hello propriétaire de groupe du dossier parent de hello sous le hello nouveau fichier ou dossier est créé.

### <a name="i-am-hello-owning-user-of-a-file-but-i-dont-have-hello-rwx-permissions-i-need-what-do-i-do"></a>Je suis hello propriétaire de l’utilisateur d’un fichier, mais je n’ai pas les autorisations de RWX hello qu'ai-je besoin. Que faire ?

Hello propriétaire utilisateur peut modifier les autorisations hello de hello fichier toogive eux-mêmes des autorisations RWX que dont ils ont besoin.

### <a name="when-i-look-at-acls-in-hello-azure-portal-i-see-user-names-but-through-apis-i-see-guids-why-is-that"></a>Lorsque j’examine les ACL Bonjour Azure portal je vois des noms d’utilisateur mais via des API, je vois GUID, pourquoi est-ce ?

Entrées dans les listes ACL de hello sont stockées sous forme de GUID qui correspondent toousers dans Azure AD. Hello API retournent hello GUID en l’état. Hello portail Azure tente toouse plus facile de toomake ACL par traduction hello GUID en noms conviviaux lorsque cela est possible.

### <a name="why-do-i-sometimes-see-guids-in-hello-acls-when-im-using-hello-azure-portal"></a>Parfois, pourquoi GUID dans les listes ACL de hello lorsque j’utilise hello portail Azure ?

Un GUID est affiché lorsque l’utilisateur de hello n’existe pas dans Azure AD plus. Cela se produit généralement lorsque l’utilisateur de hello a quitté l’entreprise de hello ou si son compte a été supprimé dans Azure AD.

### <a name="does-data-lake-store-support-inheritance-of-acls"></a>Data Lake Store prend-il en charge l’héritage des ACL ?

Non.

### <a name="what-is-hello-difference-between-mask-and-umask"></a>Qu’est hello différencie masque umask ?

| masque | umask|
|------|------|
| Hello **masque** propriété n’est disponible sur chaque fichier et dossier. | Hello **umask** est une propriété de hello compte Data Lake Store. Il est donc uniquement un seul umask Bonjour Data Lake Store.    |
| propriété du masque Hello sur un fichier ou un dossier peut être modifiée par hello propriétaire l’utilisateur ou le groupe d’un fichier ou un super utilisateur propriétaire. | propriété umask de Hello ne peut pas être modifiée par n’importe quel utilisateur, même un super utilisateur. Il s’agit d’une valeur constante non modifiable.|
| propriété du masque Hello est utilisée au cours de l’algorithme de vérification d’accès hello au runtime toodetermine si l’utilisateur dispose de tooperform de droite hello des opérations sur un fichier ou dossier. rôle Hello du masque de hello est toocreate « autorisations effectives » au moment de hello de vérification d’accès. | Hello umask n’est pas utilisé lors de la vérification d’accès du tout. Hello umask est utilisé toodetermine hello accès ACL de nouveaux éléments enfants d’un dossier. |
| masque de Hello est une valeur RWX de 3 bits qui s’applique utilisateur propriétaire, groupe nommé et toonamed utilisateur au moment de hello de vérification d’accès.| umask Hello est une valeur de 9 bits qui s’applique toohello utilisateur, groupe, propriétaire propriétaire et **autres** d’un nouvel enfant.|

### <a name="where-can-i-learn-more-about-posix-access-control-model"></a>Comment en savoir plus sur le modèle de contrôle d’accès POSIX ?

* [Listes de contrôle d’accès (ACL) POSIX sur Linux](http://www.vanemery.com/Linux/ACL/POSIX_ACL_on_Linux.html)

* [HDFS Permission Guide (Guide des autorisations HDFS)](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html)

* [Forum aux questions POSIX](http://www.opengroup.org/austin/papers/posix_faq.html)

* [POSIX 1003.1 2008](http://standards.ieee.org/findstds/standard/1003.1-2008.html)

* [POSIX 1003.1 2013](http://pubs.opengroup.org/onlinepubs/9699919799.2013edition/)

* [POSIX 1003.1 2016](http://pubs.opengroup.org/onlinepubs/9699919799.2016edition/)

* [ACL POSIX sous Ubuntu](https://help.ubuntu.com/community/FilePermissionsACLs)

* [ACL using access control lists on Linux (ACL utilisant des listes de contrôle d’accès sous Linux)](http://bencane.com/2012/05/27/acl-using-access-control-lists-on-linux/)

## <a name="see-also"></a>Voir aussi

* [Présentation d’Azure Data Lake Store](data-lake-store-overview.md)
