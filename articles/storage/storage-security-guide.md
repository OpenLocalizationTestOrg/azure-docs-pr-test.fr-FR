---
title: "guide de sécurité de stockage aaaAzure | Documents Microsoft"
description: "Détails hello de nombreuses méthodes de sécurisation du stockage Azure, y compris mais non limité tooRBAC, chiffrement de Service de stockage, chiffrement côté Client, SMB 3.0 et chiffrement de disque Azure."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 6f931d94-ef5a-44c6-b1d9-8a3c9c327fb2
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: d406ff0d6b45c6107d0276ad9e65c331078ce792
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-security-guide"></a>Guide de sécurité Azure Storage
## <a name="overview"></a>Vue d'ensemble
Le stockage Azure fournit un ensemble complet des fonctionnalités de sécurité qui en permettent aux développeurs de toobuild des applications sécurisées. compte de stockage Hello lui-même peut être sécurisé à l’aide du contrôle d’accès en fonction du rôle et Azure Active Directory. Les données peuvent être sécurisées en transit entre une application et Azure au moyen du [chiffrement côté client](storage-client-side-encryption.md), de HTTPS ou de SMB 3.0. Donnée peut être définie toobe automatiquement chiffrée lorsque écrite à l’aide du stockage tooAzure [chiffrement de Service de stockage (SSE)](storage-service-encryption.md). Les disques du système d’exploitation et les données utilisées par les ordinateurs virtuels peuvent être définies toobe chiffré à l’aide [chiffrement de disque Azure](../security/azure-security-disk-encryption.md). Accès délégué toohello les objets de données dans le stockage Azure peuvent être accordées à l’aide de [Signatures d’accès partagé](storage-dotnet-shared-access-signature-part-1.md).

Cet article fournit une vue d’ensemble sur chacune de ces fonctionnalités de sécurité, qui peuvent être utilisées avec Azure Storage. Des liens sont fournis tooarticles qui vous donne des détails de chaque fonctionnalité et vous pouvez facilement faire des investigations sur chaque rubrique.

Voici hello toobe de rubriques abordée dans cet article :

* [Sécurité du plan de gestion](#management-plane-security) – Sécurisation de votre compte de stockage

  plan de gestion Hello compose de hello ressources utilisées toomanage à votre compte de stockage. Dans cette section, nous parlerons de modèle de déploiement du Gestionnaire de ressources Azure hello et comment accéder à des comptes de stockage tooyour toocontrol de contrôle d’accès en fonction du rôle (RBAC) toouse. Nous aborderons également la gestion des clés de votre compte de stockage et comment tooregenerate les.
* [Plan de sécurité des données](#data-plane-security) – tooYour d’accès de sécurisation des données

  Dans cette section, nous allons examiner autorisant l’accès toohello les objets de données réelles dans votre compte de stockage, tels que les objets BLOB, les fichiers, les files d’attente et les tables, à l’aide de stratégies d’accès stockée et de Signatures d’accès partagé. Nous évoquerons à la fois les signatures d’accès partagé (SAP) au niveau des services et les signatures d’accès partagé au niveau des comptes. Nous verrons comment toolimit accéder à adresse IP spécifique de tooa (ou la plage d’adresses IP), le protocole de hello toolimit utilisé tooHTTPS et découvrez comment toorevoke une Signature d’accès partagé sans attendre tooexpire.
* [Chiffrement en transit](#encryption-in-transit)

  Cette section explique comment les données toosecure lorsque vous le transférez dans ou hors d’Azure Storage. Nous parlerons hello recommandé d’utiliser de chiffrement hello et HTTPS utilisé par SMB 3.0 pour les partages de fichiers Azure. Nous allons également au chiffrement côté Client, ce qui vous permet de tooencrypt hello données avant leur transfert vers le stockage dans une application cliente et toodecrypt hello après leur transfert hors stockage.
* [Chiffrement au repos](#encryption-at-rest)

  Nous aborderons le chiffrement de Service de stockage (SSE), et comment vous pouvez l’activer pour un compte de stockage, vos objets BLOB de blocs, objets BLOB de pages, ce qui entraîne et ajouter des objets BLOB automatiquement chiffrée tooAzure stockage lors de l’écriture. Nous examinerons également comment vous pouvez utiliser le chiffrement de disque Azure et Explorer les différences de base hello et les cas de chiffrement de disque et SSE et le chiffrement côté Client. Nous nous pencherons brièvement sur la conformité aux normes FIPS des ordinateurs de l’administration américaine.
* À l’aide de [stockage Analytique](#storage-analytics) accès tooaudit du stockage Azure

  Cette section décrit le mode de journalisation des informations toofind dans analytique de stockage hello pour une demande. Nous examinons analytique de stockage réel des données de journal et voir comment toodiscern si une demande est faite avec hello stockage clé, avec une signature d’accès partagé, de compte ou anonyme et si elle a réussi ou échoué.
* [Activation de clients basés sur le navigateur à l’aide de CORS](#Cross-Origin-Resource-Sharing-CORS)

  Cette section traite de la ressource de cross-origine tooallow partage (CORS). Nous parlerons accès inter-domaines et comment toohandle avec les fonctionnalités CORS hello créée dans le stockage Azure.

## <a name="management-plane-security"></a>Sécurité du plan de gestion
plan de gestion Hello se compose d’opérations qui affectent le compte de stockage hello lui-même. Par exemple, vous pouvez créer ou supprimer un compte de stockage, obtenir la liste des comptes de stockage dans un abonnement, récupérer les clés de compte de stockage hello ou régénérer les clés de compte de stockage hello.

Quand vous créez un compte de stockage, vous sélectionnez un modèle de déploiement Classique ou Resource Manager. modèle classique de Hello de création de ressources dans Azure permet uniquement d’abonnement de toohello accès tout ou rien et à son tour, hello compte de stockage.

Ce guide se concentre sur le modèle de gestionnaire de ressources hello qui est hello recommandé moyen permettant de créer des comptes de stockage. Avec les comptes de stockage du Gestionnaire de ressources hello, plutôt que d’abonnement de donnant accès toohello entière, vous pouvez contrôler l’accès sur un plan de gestion au niveau toohello plus limité à l’aide du contrôle d’accès en fonction du rôle (RBAC).

### <a name="how-toosecure-your-storage-account-with-role-based-access-control-rbac"></a>Comment toosecure votre compte de stockage avec le contrôle d’accès en fonction du rôle (RBAC)
Pour commencer, expliquons ce qu’est RBAC et voyons comment l’utiliser. À chaque abonnement Azure correspond un annuaire Azure Active Directory. Les utilisateurs, des groupes et des applications à partir de ce répertoire peuvent être accordées à accéder aux toomanage ressources hello abonnement Azure qui utilisent le modèle de déploiement du Gestionnaire de ressources hello. Il s’agit de visé tooas contrôle d’accès en fonction du rôle (RBAC). toomanage cela accéder, vous pouvez utiliser hello [portail Azure](https://portal.azure.com/), hello [outils CLI d’Azure](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), ou hello [API REST de fournisseur de ressources de stockage Azure ](https://msdn.microsoft.com/library/azure/mt163683.aspx).

Avec le modèle de gestionnaire de ressources hello, vous placez le compte de stockage hello dans une ressource groupe et contrôle d’accès toohello Gestion plan de ce compte de stockage spécifique à l’aide d’Azure Active Directory. Vous pouvez par exemple, donner à des utilisateurs spécifiques hello capacité tooaccess hello clés compte de stockage, tandis que d’autres utilisateurs peuvent afficher les informations de compte de stockage hello, mais ne peut pas accéder aux clés de compte de stockage hello.

#### <a name="granting-access"></a>Octroi de l’accès
L’accès est accordé en assignant hello toousers du rôle RBAC appropriés, les groupes et les applications, à la portée de droite hello. toogrant accès toohello tout abonnement, vous affectez un rôle au niveau d’abonnement hello. Vous pouvez accorder tooall d’accès des ressources hello dans un groupe de ressources en accordant des autorisations toohello ressource groupe. Vous pouvez également affecter des rôles spécifiques des ressources de toospecific, telles que les comptes de stockage.

Voici les points principaux hello que vous devez tooknow sur l’utilisation des opérations de gestion RBAC tooaccess hello d’un compte de stockage Azure :

* Lorsque vous affectez des accès, vous affectez en fait un compte de toohello de rôle que vous souhaitez toohave accès. Vous pouvez contrôler l’accès toohello opérations utilisées toomanage ce compte de stockage, mais pas les données toohello des objets dans le compte de hello. Par exemple, vous pouvez accorder l’autorisation tooretrieve des propriétés de hello de compte de stockage hello (telles que la redondance), mais pas tooa conteneur ou de données dans un conteneur de stockage d’objets Blob.
* Pour une personne toohave autorisation tooaccess hello hello compte de stockage des objets de données, vous pouvez leur donner des clés du compte de stockage autorisation tooread hello et cet utilisateur peut utiliser ensuite ces objets BLOB de clés tooaccess hello, les files d’attente, les tables et les fichiers.
* Rôles peuvent être attribués tooa compte d’utilisateur spécifique, à un groupe d’utilisateurs ou d’application spécifique de tooa.
* À chaque rôle correspond une liste d’actions et de non-actions. Par exemple, rôle de Machine virtuelle collaborateur hello a une Action de « listKeys » qui permet de lire des toobe de clés de compte de stockage hello. Hello collaborateur a « Pas d’Actions » telles que la mise à jour de l’accès pour les utilisateurs dans Active Directory de hello hello.
* Rôles pour le stockage inclure (mais ne sont pas limitées à) suivant de hello :

  * Propriétaire : il peut tout gérer, y compris l’accès.
  * Collaborateurs : ils peuvent le faire quoi que ce soit propriétaire de hello excepté permettre accorder un accès. Une personne disposant de ce rôle permettre afficher et régénérer les clés de compte de stockage hello. Avec des clés de compte de stockage hello, ils peuvent accéder à des objets de données hello.
  * Lecteur : ils peuvent afficher les informations de compte de stockage hello, à l’exception des clés secrètes. Par exemple, si vous attribuez un rôle disposant d’autorisations de lecture sur toosomeone de compte de stockage hello, ils peuvent afficher les propriétés de hello hello du compte de stockage, mais ils ne peuvent pas apporter des modifications de propriétés de toohello ou afficher les clés de compte de stockage hello.
  * Collaborateur du compte de stockage : ils peuvent gérer un compte de stockage hello : ils peuvent lire hello des groupes de ressources et des ressources, de l’abonnement et de créer et de gérer les déploiements de groupe de ressources abonnement. Ils peuvent également accéder aux clés de compte de stockage hello, qui à son tour signifie qu’ils peuvent accéder à plan de données hello.
  * Administrateur de l’accès utilisateur : ils peuvent gérer le compte de stockage de toohello accès utilisateur. Par exemple, ils pourront accorder à utilisateur de lecteur accès tooa spécifique.
  * Contributeur de la Machine virtuelle : ils peuvent gérer des ordinateurs virtuels, mais pas hello stockage compte toowhich qu’ils sont connectés. Ce rôle peut répertorier les clés de compte de stockage hello, ce qui signifie que hello toowhom utilisateur vous attribuez ce rôle peut mettre à jour le plan de données hello.

    Dans l’ordre pour un utilisateur de toocreate un ordinateur virtuel, ils ont toobe toocreate en mesure de hello correspondant VHD fichier un compte de stockage. toodo, dont ils ont besoin de stockage de hello toobe tooretrieve en mesure de clé de compte et lui passer API toohello création hello machine virtuelle. Par conséquent, ils doivent avoir cette autorisation pour vous pouvez répertorier les clés de compte de stockage hello.
* des rôles personnalisés Hello capacité toodefine est une fonctionnalité qui vous permet de toocompose un ensemble d’actions dans une liste des actions disponibles qui peuvent être effectuées sur les ressources Azure.
* l’utilisateur Hello a toobe défini dans Azure Active Directory avant de pouvoir affecter un toothem de rôle.
* Vous pouvez créer un rapport qui accordées/révoquées le type d’accès à partir de laquelle et sur l’étendue à l’aide de PowerShell ou hello CLI d’Azure.

#### <a name="resources"></a>Ressources
* [Contrôle d’accès en fonction du rôle Azure Active Directory](../active-directory/role-based-access-control-configure.md)

  Cet article explique hello de contrôle d’accès basé sur un rôle Active Directory de Azure et de son fonctionnement.
* [RBAC : rôles intégrés](../active-directory/role-based-access-built-in-roles.md)

  Cet article décrit en détail tous les rôles intégrés de hello disponibles dans RBAC.
* [Présentation du déploiement de Resource Manager et du déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md)

  Cet article explique le déploiement du Gestionnaire de ressources hello et modèles de déploiement classique et explique les avantages de hello de l’utilisation de groupes de gestion de ressources et les ressources hello. Il explique le fonctionnement de hello Azure Compute, réseau et les fournisseurs de stockage en mode de gestionnaire de ressources hello.
* [Gestion du contrôle d’accès en fonction du rôle avec l’API REST de hello](../active-directory/role-based-access-control-manage-access-rest.md)

  Cet article explique comment toouse hello API REST toomanage RBAC.
* [Informations de référence sur l’API REST du fournisseur de ressources Azure Storage](https://msdn.microsoft.com/library/azure/mt163683.aspx)

  Il s’agit de référence hello pour hello API que vous pouvez utiliser toomanage votre compte de stockage par programme.
* [Tooauth du guide du développeur avec des API Azure Resource Manager](http://www.dushyantgill.com/blog/2015/05/23/developers-guide-to-auth-with-azure-resource-manager-api/)

  Cet article explique comment à l’aide de tooauthenticate hello des API du Gestionnaire de ressources.
* [Role-Based Access Control for Microsoft Azure from Ignite (Contrôle d’accès en fonction du rôle pour Microsoft Azure)](https://channel9.msdn.com/events/Ignite/2015/BRK2707)

  Il s’agit d’un lien de tooa vidéo sur Channel 9 à partir de la conférence de Ignite 2015 MS hello. Dans cette session, ils parlent accéder aux fonctionnalités de gestion et création de rapports dans Azure et Explorer les meilleures pratiques pour la sécurisation de l’accès tooAzure les abonnements à l’aide d’Azure Active Directory.

### <a name="managing-your-storage-account-keys"></a>Gestion des clés de compte de stockage
Compte de stockage clés sont des chaînes de 512 bits créés par Azure qui, en même temps que le stockage de hello nom, du compte peut être utilisé tooaccess hello des objets stockés dans le compte de stockage hello, par exemple, les objets BLOB, les entités au sein d’une table, les messages de file d’attente et les fichiers sur un partage de fichiers Azure. Contrôle toohello stockage compte clés des contrôles d’accès accéder au plan de données toohello pour ce compte de stockage.

Chaque compte de stockage a deux clés visés tooas « Clé 1 » et « 2 de la clé » Bonjour [portail Azure](http://portal.azure.com/) et Bonjour applets de commande PowerShell. Ceux-ci peuvent être régénérées manuellement à l’aide d’une des méthodes, y compris, mais non limité toousing hello [portail Azure](https://portal.azure.com/), PowerShell, hello CLI d’Azure ou par programme à l’aide de hello bibliothèque cliente de stockage .NET ou hello Azure API REST des Services de stockage.

Il existe un nombre quelconque de raisons tooregenerate vos clés de compte de stockage.

* Vous pouvez souhaiter les régénérer à intervalles réguliers pour des raisons de sécurité.
* Vous serez régénérer vos clés de compte de stockage si un utilisateur géré toohack dans une application et récupérer la clé de hello qui a été codé en dur ou enregistré dans un fichier de configuration, en leur donnant un compte de stockage tooyour un accès complet.
* Un autre cas de régénération de la clé est si votre équipe utilise une application de l’Explorateur de stockage qui conserve la clé de compte de stockage hello, et un des membres de l’équipe hello conserve. application Hello continue toowork, en leur donnant accès tooyour stockage compte une fois qu’ils ne disparaissent. Il s’agit réellement hello recherché qu’ils ont créées au niveau du compte de Signatures d’accès partagé : vous pouvez utiliser une SAP au niveau du compte au lieu de stocker les clés d’accès hello dans un fichier de configuration.

#### <a name="key-regeneration-plan"></a>Plan de régénération de clé
Vous ne souhaitez pas clé de régénérer hello toojust que vous utilisez sans une planification. Si vous procédez ainsi, vous a coupé tous les accès toothat compte de stockage qui peut provoquer une interruption majeure. C’est la raison pour laquelle il existe deux clés. Nous vous recommandons de régénérer une seule clé à la fois.

Avant de régénérer vos clés, veillez à ce que vous avez une liste de toutes les applications qui dépendent de compte de stockage hello, ainsi que d’autres services que vous utilisez dans Azure. Par exemple, si vous utilisez Azure Media Services qui dépendent de votre compte de stockage, vous devez resynchroniser les clés d’accès hello avec votre service multimédia après avoir régénéré la clé de hello. Si vous utilisez des applications telles que l’Explorateur de stockage, vous devez tooprovide hello nouvelles clés toothose également les applications. Notez que si vous avez des ordinateurs virtuels dont les fichiers VHD sont stockés dans le compte de stockage hello, il n’est pas affecté par la régénération des clés de compte de stockage hello.

Vous pouvez régénérer vos clés Bonjour portail Azure. Une fois que les clés sont régénérées qu’ils peuvent occuper too10 minutes toobe synchronisés entre les Services de stockage.

Lorsque vous êtes prêt, hello général le processus sont détaillant la façon dont vous devez modifier votre clé. Dans ce cas, les hypothèses hello est que vous utilisez actuellement Key 1 et que vous vous apprêtez toochange tout toouse clé 2 à la place.

1. Régénérer tooensure clé 2 qu’il est sécurisé. Vous pouvez le faire dans hello portail Azure.
2. Dans toutes les applications hello emplacement de stockage de clé de stockage de hello, modifiez la valeur de nouveau de hello stockage toouse clé clé 2. Testez et publiez l’application hello.
3. Une fois toutes les Hello applications et services sont activés et en cours d’exécution avec succès, régénérer la clé 1. Cela garantit que toute personne toowhom vous n’avez pas expressément donné clé hello n’aura plus accéder au compte de stockage toohello.

Si vous utilisez actuellement la clé 2, vous pouvez utiliser hello même processus, mais les noms de clés hello inverse.

Vous pouvez migrer sur quelques jours, la modification de chaque application toouse hello nouvelle clé et sa publication. Une fois tous les sont effectuées, puis par revenir en arrière et régénérer l’ancienne clé de hello afin qu’il ne fonctionne plus.

Une autre option est la clé de compte de stockage tooput hello dans un [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) en tant que secret et votre clé de hello de récupérer les applications à partir de là. Puis lorsque vous régénérez la clé de hello et hello Azure Key Vault de mettre à jour, les applications hello n’aurez pas toobe redéployé, car ils prennent en charge hello nouvelle clé dans Azure Key Vault de hello automatiquement. Notez que vous pouvez avoir application hello lire la clé de hello chaque fois que vous en avez besoin, ou vous pouvez mettre en cache en mémoire et en cas d’échec lors de l’utilisation, extraire la clé de hello à nouveau hello Azure Key Vault.

L’utilisation d’Azure Key Vault ajoute également un autre niveau de sécurité pour les clés de stockage. Si vous utilisez cette méthode, vous aurez jamais sont codées en dur hello stockage clé dans un fichier de configuration, ce qui supprime cette voie d’une personne l’accès des clés de toohello sans autorisation spécifique.

Un autre avantage de l’utilisation d’Azure Key Vault est que vous pouvez également contrôler les clés d’accès tooyour à l’aide d’Azure Active Directory. Cela signifie que vous pouvez accorder quelques toohello accès applications besoin des clés de hello tooretrieve d’Azure Key Vault, sachez que les autres applications seront pas en mesure de tooaccess des clés de hello sans leur accorder l’autorisation en particulier.

Remarque : il est recommandé de toouse uniquement un des hello les clés dans toutes vos applications à hello même temps. Si vous utilisez la clé de 1 à certains endroits et touche 2 dans d’autres, à ne pas être en mesure de toorotate vos clés d’une application de perdre l’accès.

#### <a name="resources"></a>Ressources
* [À propos des comptes Azure Storage](storage-create-storage-account.md#regenerate-storage-access-keys)

  Cet article présente une vue d’ensemble des comptes de stockage et décrit l’affichage, la copie et la régénération des clés d’accès de stockage.
* [Informations de référence sur l’API REST du fournisseur de ressources Azure Storage](https://msdn.microsoft.com/library/mt163683.aspx)

  Cet article contient des articles de toospecific de liens sur la récupération des clés de compte de stockage hello et les clés de compte de stockage hello régénération d’un compte Azure à l’aide des API REST de hello. Remarque : ceci concerne les comptes de stockage Resource Manager.
* [Opérations sur les comptes de stockage](https://msdn.microsoft.com/library/ee460790.aspx)

  Cet article Bonjour référence d’API REST Gestionnaire de Service de stockage contient des articles de toospecific de liens sur la récupération et la régénération de clés de compte de stockage hello à l’aide des API REST de hello. Remarque : Il s’agit des comptes de stockage classique hello.
* [Dire la gestion de tookey goodbye : gestion des données de stockage tooAzure access à l’aide d’Azure AD](http://www.dushyantgill.com/blog/2015/04/26/say-goodbye-to-key-management-manage-access-to-azure-storage-data-using-azure-ad/)

  Cet article explique comment toouse Active Directory toocontrol accéder aux clés de stockage Azure tooyour dans Azure Key Vault. Il montre également comment toouse un Azure Automation clés de hello tooregenerate toutes les heures de travail.

## <a name="data-plane-security"></a>Sécurité du plan de données
Plan de sécurité des données fait référence à des méthodes toohello toosecure utilisé hello des objets stockés dans le stockage Azure – fichiers, les files d’attente, les tables et les objets BLOB de hello. Nous avons vu tooencrypt données hello et la sécurité pendant le transit des données de hello, mais comment procéder à l’autorisation d’accès toohello objets ?

Il existe deux méthodes de contrôle accès toohello pour les objets d’eux-mêmes. Hello est tout d’abord par contrôle clés de compte de stockage accès toohello et hello est ensuite utilisant des objets de données de Signatures d’accès partagé toogrant accès toospecific pour une durée spécifique.

Une exception toonote est que vous pouvez autoriser un accès public tooyour BLOB en définissant le niveau d’accès hello pour le conteneur de hello contenant des objets BLOB de hello en conséquence. Si vous définissez l’accès pour un conteneur tooBlob ou le conteneur, elle permet un accès en lecture public pour les objets BLOB de hello dans le conteneur. Cela signifie que toute personne disposant d’une URL pointant blob tooa dans le conteneur peut l’ouvrir dans un navigateur sans les clés de compte de stockage hello ou à l’aide d’une Signature d’accès partagé.

### <a name="storage-account-keys"></a>Clés de compte de stockage
Clés de compte de stockage sont des chaînes de 512 bits créés par Azure qui, avec le nom de compte de stockage hello, peut être utilisé tooaccess hello des objets stockés dans le compte de stockage hello.

Par exemple, vous pouvez lire les objets BLOB, écrire tooqueues, créer des tables et modifier des fichiers. Nombre de ces actions peuvent être réalisées via hello Azure portal, ou en utilisant l’une des nombreuses applications de l’Explorateur de stockage. Vous pouvez également écrire hello toouse de code API REST ou de l’un des tooperform de bibliothèques clientes de stockage hello ces opérations.

Comme indiqué dans la section de hello sur hello [sécurité du plan d’administration](#management-plane-security), accéder aux clés de stockage toohello pour un compte de stockage standard peut être accordé en donnant un accès complet toohello abonnement Azure. Les clés d’accès toohello stockage pour un compte de stockage à l’aide du modèle de gestionnaire de ressources Azure hello peuvent être contrôlés via le contrôle d’accès en fonction du rôle (RBAC).

### <a name="how-toodelegate-access-tooobjects-in-your-account-using-shared-access-signatures-and-stored-access-policies"></a>Comment toodelegate aux tooobjects dans votre compte à l’aide de stratégies d’accès stockée et de Signatures d’accès partagé
Une Signature d’accès partagé est une chaîne qui contient un jeton de sécurité qui peut être attachés tooa URI qui vous permet du toostorage toodelegate accéder aux objets et spécifier des contraintes telles que les autorisations hello et la plage de date/heure hello d’accès.

Vous pouvez accorder des accès tooblobs, les conteneurs, les messages de file d’attente, les fichiers et les tables. Avec les tables, vous pouvez réellement accorder autorisation tooaccess une plage d’entités dans la table de hello en spécifiant hello partition et ligne plages de clés toowhich vous souhaitez l’accès utilisateur toohave hello. Par exemple, si vous avez des données stockées avec une clé de partition de l’état géographique, vous pouvez accorder une personne accéder aux données de hello toojust de Californie.

Dans un autre exemple, vous pouvez donner à une application web à un jeton SAS qui lui permet de file d’attente de toowrite entrées tooa et permettre à un processus de travail application de rôle, un message de tooget jeton SAS de hello en file d’attente et de les traite. Ou vous pouvez donner à un client un jeton SAP ils peuvent utiliser un conteneur de tooa tooupload images dans le stockage Blob et donner un tooread de permission d’application web de ces images. Dans les deux cas, il existe une séparation des préoccupations – accès hello simplement dont ils ont besoin dans peut être accordée à chaque application commande tooperform leurs tâches. Cela est possible via l’utilisation de hello de Signatures d’accès partagé.

#### <a name="why-you-want-toouse-shared-access-signatures"></a>Raison pour laquelle vous souhaitez toouse les Signatures d’accès partagé
Pourquoi vous souhaiteriez toouse un SAS au lieu de simplement vous communiquez votre clé de compte de stockage, qui est beaucoup plus facile ? Vous communiquez votre clé de compte de stockage est tels que le partage de clés hello de Royaume de votre stockage. L’accès accordé est complet. Une personne peut utiliser vos clés et télécharger son compte de stockage de musique bibliothèque tooyour. Elle peut également remplacer vos fichiers par des versions infectées par des virus, ou voler vos données. Révéler le compte de stockage tooyour un accès illimité est un élément qui ne doit pas être prise à la légère.

Avec les Signatures d’accès partagé, vous pouvez donner à un client uniquement les autorisations hello requises pour une durée limitée. Par exemple, si un utilisateur télécharge un compte tooyour d’objets blob, vous pouvez accorder les accès en écriture pour juste assez blob de hello tooupload heure (selon taille hello d’objet blob hello, bien sûr). Si vous changez ensuite d’avis, vous pouvez révoquer cet accès.

En outre, vous pouvez spécifier que les demandes effectuées à l’aide d’un SAS sont restreinte tooa certaine tooAzure externe de plage d’adresses IP ou adresse IP. Vous pouvez également exiger que les demandes soient effectuées à l’aide d’un protocole spécifique (HTTPS ou HTTP/HTTPS). Cela signifie que si vous ne souhaitez que le trafic HTTPS tooallow, vous pouvez définir hello requis protocole tooHTTPS uniquement, et le trafic HTTP sera bloqué.

#### <a name="definition-of-a-shared-access-signature"></a>Définition d’une signature d’accès partagé
Une Signature d’accès partagé est qu'un ensemble de paramètres de requête ajouté toohello les URL pointant vers des ressources de hello

qui fournit des informations sur l’accès de hello autorisant et hello durée pour le hello l’accès est autorisé. Voici un exemple ; Cet URI fournit un accès en lecture tooa blob pendant cinq minutes. Notez que les paramètres de requête SAP doivent être encodés dans une URL, par exemple %3A pour le signe deux-points (:) ou %20 pour un espace.

```
http://mystorage.blob.core.windows.net/mycontainer/myblob.txt (URL toohello blob)
?sv=2015-04-05 (storage service version)
&st=2015-12-10T22%3A18%3A26Z (start time, in UTC time and URL encoded)
&se=2015-12-10T22%3A23%3A26Z (end time, in UTC time and URL encoded)
&sr=b (resource is a blob)
&sp=r (read access)
&sip=168.1.5.60-168.1.5.70 (requests can only come from this range of IP addresses)
&spr=https (only allow HTTPS requests)
&sig=Z%2FRHIX5Xcg0Mq2rqI3OlWTjEg2tYkboXr1P9ZUXDtkk%3D (signature used for hello authentication of hello SAS)
```

#### <a name="how-hello-shared-access-signature-is-authenticated-by-hello-azure-storage-service"></a>Comment hello Signature d’accès partagé est authentifiée par hello Service de stockage Azure
Lorsque le service de stockage hello reçoit la demande de hello, il accepte des paramètres de requête d’entrée hello et crée une signature à l’aide de hello même méthode que hello programme appelant. Il compare ensuite les signatures de deux hello. Si elles conviennent, hello service de stockage peut vérifier hello stockage service version toomake qu’elle est valide, vérifiez que hello date et heure actuelles sont dans la fenêtre spécifiée hello, accès hello assurer de marque demandé correspond demande toohello, etc..

Par exemple, avec nos URL ci-dessus, si hello URL a été pointe le fichier tooa au lieu d’un objet blob, cette demande échoue car elle spécifie que hello que signature d’accès partagé est pour un objet blob. Si hello commande REST appelée a été tooupdate un objet blob, il échoue car hello Signature d’accès partagé Spécifie que l’accès en lecture seule est autorisé.

#### <a name="types-of-shared-access-signatures"></a>Types de signatures d’accès partagé
* Une SAP de niveau de service peut être utilisé tooaccess des ressources spécifiques dans un compte de stockage. Quelques exemples de ce sont récupération d’une liste d’objets BLOB dans un conteneur, un objet blob est téléchargé, mise à jour une entité dans une table, en ajoutant file d’attente de messages tooa ou téléchargement d’un partage de fichiers de tooa de fichier.
* Une SAP au niveau du compte peut être utilisé tooaccess toute une SAP de niveau de service peut être utilisée pour. En outre, elle peut octroyer à tooresources d’options qui ne sont pas autorisées avec une SAP de niveau de service, tels que les conteneurs de toocreate possibilité hello, tables, files d’attente et les partages de fichiers. Vous pouvez également spécifier les services toomultiple d’accès à la fois. Par exemple, vous pouvez donner un accès tooboth BLOB et les fichiers dans votre compte de stockage.

#### <a name="creating-an-sas-uri"></a>Création d’un URI SAP
1. Vous pouvez créer un URI ad hoc à la demande, définir l’ensemble des paramètres de requête hello chaque fois.

   Cette opération est vraiment flexible mais, si vous avez un ensemble logique de paramètres qui sont chaque fois similaires, il est plus judicieux d’utiliser une stratégie d’accès stockée.
2. Vous pouvez créer une stratégie d’accès stockée pour un conteneur entier, un partage de fichiers, une table ou une file d’attente. Puis vous pouvez utiliser cela comme point de départ hello pour hello URI SAS vous créez. Les autorisations basées sur les stratégies d’accès stockées peuvent être facilement révoquées. Vous pouvez avoir jusqu'à too5 les stratégies définies sur chaque conteneur, une file d’attente, un tableau ou un partage de fichiers.

   Par exemple, si vous vouliez toohave de nombreuses personnes lire les objets BLOB de hello dans un conteneur spécifique, vous pouvez créer une stratégie d’accès stockée indiquant que « accorder l’accès en lecture » et tous les autres paramètres qui seront hello même chaque fois. Vous pouvez ensuite créer un URI SAS en utilisant les paramètres de hello Hello stratégie d’accès stockée et en spécifiant les hello la date/heure d’expiration. Hello parti de cela est que vous n’avez toospecify paramètres toutes hello requête chaque fois.

#### <a name="revocation"></a>Révocation
Supposons que votre SAP a été compromis ou si vous souhaitez toochange il en raison de la sécurité de l’entreprise ou des exigences de conformité réglementaire. Comment révoquer des ressources de tooa accès à l’aide de cette SAS ? Il convient de création hello URI SAS.

Si vous utilisez des URI appropriés, vous avez trois possibilités. Vous pouvez émettre des jetons SAP avec des stratégies d’expiration court et attendez simplement hello SAS tooexpire. Vous pouvez renommer ou supprimer la ressource hello (en supposant que jeton de hello a été étendue tooa seul objet). Vous pouvez modifier les clés de compte de stockage hello. Cette dernière option peut entraîner de graves problèmes, en fonction du nombre de services est à l’aide de ce compte de stockage et probablement n’est pas un que choix toodo sans une planification.

Si vous utilisez un SAS dérivé d’une stratégie d’accès stockée, vous pouvez supprimer l’accès en révoquant hello stratégie d’accès stockée : vous pouvez simplement modifier afin qu’il a déjà expiré, ou vous pouvez le supprimer complètement. Cette opération prend effet immédiatement et invalide toutes les signatures d’accès partagé créées à l’aide de cette stratégie d’accès stockée. Mise à jour ou suppression hello stratégie d’accès stockée peut affecter les utilisateurs d’accéder à ce conteneur spécifique, un partage de fichiers, une table ou une file d’attente via SAS, mais si hello concernent les clients afin qu’ils demandent une nouvelle SAP lorsque hello ancien devient non valide, cela fonctionne correctement.

À l’aide d’un SAS dérivé d’une stratégie d’accès stockée vous donne en effet toorevoke de capacité hello que SAS immédiatement, il est hello recommandé de meilleure pratique tooalways utiliser des stratégies d’accès stockées lorsque cela est possible.

#### <a name="resources"></a>Ressources
Pour plus d’informations sur l’utilisation de Signatures d’accès partagé et stockées les stratégies d’accès complet des exemples, reportez-vous à toohello suivant des articles :

* Il s’agit d’articles de référence hello.

  * [Exemples d’associations de sécurité de service](https://msdn.microsoft.com/library/dn140256.aspx)

    Cet article fournit des exemples d’utilisation d’une signature d’accès partagé de niveau service avec des objets blob, des messages de file d’attente, des plages de tables et des fichiers.
  * [Construction d’un service SAP](https://msdn.microsoft.com/library/dn140255.aspx)
  * [Construction d’un compte SAP](https://msdn.microsoft.com/library/mt584140.aspx)
* Il s’agit des didacticiels pour l’utilisation de hello .NET client bibliothèque toocreate Signatures d’accès partagées et des stratégies d’accès stockée.

  * [Utilisation des signatures d’accès partagé (SAP)](storage-dotnet-shared-access-signature-part-1.md)
  * [Partagé des Signatures d’accès, partie 2 : Créer et utiliser une SAP avec hello Service Blob](storage-dotnet-shared-access-signature-part-2.md)

    Cet article contient une explication du modèle SAS de hello, exemples de Signatures d’accès partagé, et les recommandations de meilleure pratique de hello utilisent de SAP. Vous trouverez également révocation hello d’autorisation hello.
* Limitation de l’accès par adresse IP (listes ACL IP)

  * [Qu’est-ce qu’une liste de contrôle d’accès de point de terminaison (ACL) ?](../virtual-network/virtual-networks-acl.md)
  * [Construction d’un service SAP](https://msdn.microsoft.com/library/azure/dn140255.aspx)

    Il s’agit d’article de référence hello pour les associations de sécurité de niveau de service ; Elle inclut un exemple de création de liste ACL IP.
  * [Construction d’un compte SAP](https://msdn.microsoft.com/library/azure/mt584140.aspx)

    Il s’agit d’article de référence hello pour les associations de sécurité au niveau des comptes ; Elle inclut un exemple de création de liste ACL IP.
* Authentification

  * [Authentification pour hello Services de stockage Azure](https://msdn.microsoft.com/library/azure/dd179428.aspx)
* Didacticiel de prise en main des signatures d’accès partagé

  * [SAS Getting Started Tutorial (Didacticiel de prise en main des signatures d’accès partagé)](https://github.com/Azure-Samples/storage-dotnet-sas-getting-started)

## <a name="encryption-in-transit"></a>Chiffrement en transit
### <a name="transport-level-encryption--using-https"></a>Chiffrement au niveau du transport – Utilisation de HTTPS
Une autre étape, vous devez prendre la sécurité de hello tooensure de vos données de stockage Azure donnée tooencrypt hello entre le client de hello et de stockage Azure. Il est recommandé de première Hello tooalways utiliser hello [HTTPS](https://en.wikipedia.org/wiki/HTTPS) protocole, ce qui garantit une communication sécurisée sur hello Internet public.

toohave un canal de communication sécurisé, vous devez toujours utiliser HTTPS lors de l’appel d’API REST de hello ou l’accès à des objets dans le stockage. En outre, **Signatures d’accès partagé**, ce qui peut être utilisé toodelegate accéder aux objets de stockage tooAzure, inclure une option toospecify que hello uniquement le protocole HTTPS peut être utilisé lors de l’utilisation de Signatures d’accès partagé, en s’assurant que toute personne envoi de liens avec des jetons SAS utilisera le protocole approprié de hello.

Vous pouvez appliquer utilisation hello du protocole HTTPS lors de l’appel d’objets de tooaccess d’API REST hello dans les comptes de stockage en activant [sécuriser le transfert requis](storage-require-secure-transfer.md) hello compte de stockage. Les connexions utilisant le protocole HTTP seront refusées une fois cette option activée.

### <a name="using-encryption-during-transit-with-azure-file-shares"></a>Utilisation du chiffrement pendant le transit avec des partages de fichiers Azure
Stockage de fichier Azure prend en charge HTTPS lors de l’utilisation des API REST de hello, mais il est plus couramment utilisé comme un partage de fichiers SMB attaché tooa machine virtuelle. SMB 2.1 ne prend pas en charge le chiffrement, les connexions sont uniquement autorisées au sein de hello même région dans Azure. Toutefois, SMB 3.0 prend en charge le chiffrement et il est disponible dans Windows Server 2012 R2, Windows 8, Windows 8.1 et Windows 10, ce qui permet d’entre régions accéder et même des accès sur le bureau de hello.

Notez que tandis que les partages de fichiers Azure peuvent être utilisées avec Unix, hello client Linux SMB ne prend pas en charge le chiffrement, afin de l’accès est autorisé uniquement dans une région Azure. Prise en charge du chiffrement pour Linux est prévu hello de développeurs Linux responsables de la fonctionnalité SMB. Lorsqu’elles ajoutent le chiffrement, vous devez hello même capacité pour accéder à un partage de fichiers Azure sur Linux, comme vous le feriez pour Windows.

Vous pouvez appliquer l’utilisation de hello du chiffrement avec hello service de fichiers Azure en activant [sécuriser le transfert requis](storage-require-secure-transfer.md) hello compte de stockage. Si à l’aide de hello API REST, HTTPs est requis. Pour SMB, seules les connexions SMB qui prennent en charge le chiffrement seront établies avec succès.

#### <a name="resources"></a>Ressources
* [Comment toouse stockage Azure files avec Linux](storage-how-to-use-files-linux.md)

  Cet article explique comment toomount un fichier Azure partager sur un système et télécharger des fichiers Linux.
* [Prise en main d’Azure File Storage sur Windows](storage-dotnet-how-to-use-files.md)

  Cet article donne une vue d’ensemble de partages de fichiers Azure et comment toomount et les utiliser à l’aide de PowerShell et .NET.
* [Dans le Stockage Fichier Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)

  Cet article annonce la disponibilité générale de hello de stockage Azure et fournit des détails techniques sur le chiffrement hello SMB 3.0.

### <a name="using-client-side-encryption-toosecure-data-that-you-send-toostorage"></a>À l’aide de données de toosecure de chiffrement côté Client que vous envoyez toostorage
Le chiffrement côté client est une autre méthode possible pour garantir la sécurité de vos données pendant leur transfert entre une application cliente et Azure Storage. les données de salutation sont chiffrées avant d’être transférées dans le stockage Azure. Lorsque vous récupérez les données de salutation depuis le stockage Azure, hello sont déchiffrer les données après sa réception côté client de hello. Même si les données de salutation sont chiffrées passe sur le câble de hello, nous recommandons d’utiliser également HTTPS, car elle a des contrôles d’intégrité de données intégrées qui réduire les erreurs de réseau qui affectent l’intégrité de hello des données de hello.

Le chiffrement côté client est également une méthode de chiffrement de vos données au repos, comme les données de salutation sont stockées sous sa forme chiffrée. Nous aborderons cela plus en détail dans la section de hello sur [chiffrement au repos](#encryption-at-rest).

## <a name="encryption-at-rest"></a>Chiffrement au repos
Il existe trois fonctionnalités Azure qui fournissent un chiffrement au repos. Chiffrement de disque Azure est utilisé tooencrypt hello du système d’exploitation et des disques de données dans des Machines virtuelles IaaS. autres deux Hello : chiffrement côté Client et SSE – sont des données tooencrypt utilisé dans le stockage Azure. Nous allons étudier chacune de ces fonctionnalités, les comparer, puis déterminer quand les utiliser.

Si vous pouvez utiliser les données de chiffrement côté Client tooencrypt hello en transit (qui est également stocké sous sa forme chiffrée dans le stockage), vous pouvez préférer toosimply utilisez HTTPS pendant le transfert de hello et disposer d’un moyen pour toobe de données hello automatiquement chiffré lorsqu’il est stockées. Il existe deux façons toodo ce chiffrement de disque Azure et SSE. Un est utilisé toodirectly chiffrer les données de hello sur des disques du système d’exploitation et les données utilisées par les ordinateurs virtuels et hello autres est tooencrypt utilisé les données écrites tooAzure stockage d’objets Blob.

### <a name="storage-service-encryption-sse"></a>Storage Service Encryption (SSE)
SSE vous permet de toorequest que service de stockage hello chiffrer automatiquement des données de hello lors de l’écriture de tooAzure stockage. Lorsque vous lisez des données de salutation depuis le stockage Azure, il est déchiffré avant d’être retourné par le service de stockage hello. Cela vous permet de toosecure vos données sans avoir toomodify de code ou ajouter des applications tooany de code.

Il s’agit d’un paramètre qui s’applique le compte de stockage entier toohello. Vous pouvez activer et désactiver cette fonctionnalité en modifiant la valeur hello du paramètre de hello. toodo, vous pouvez utiliser hello du portail Azure, PowerShell, hello CLI d’Azure, hello API REST de fournisseur de ressource de stockage ou hello bibliothèque cliente de stockage .NET. Par défaut, SSE est désactivé.

À ce stade, les clés de hello utilisés pour le chiffrement de hello sont gérées par Microsoft. Nous les clés hello à l’origine et gérer le stockage sécurisé de clés de hello ainsi qu’une rotation régulière de hello hello tel que défini par la stratégie interne de Microsoft. Bonjour futures, vous obtenir hello capacité toomanage vos propres clés de chiffrement et fournir un chemin de migration à partir des clés de centres de données gérés par toocustomer des clés.

Cette fonctionnalité est disponible pour les comptes Standard et Premium stockage créés à l’aide du modèle de déploiement du Gestionnaire de ressources hello. SSE s’applique uniquement les tooblock objets BLOB, les objets BLOB de pages et ajouter des objets BLOB. Hello autres types de données, y compris les tables, les files d’attente et les fichiers ne seront pas chiffrées.

Données sont cryptées uniquement lorsque SSE est activée et les données de salutation sont écrit tooBlob stockage. L’activation ou la désactivation de SSE n’a pas d’impact sur les données existantes. En d’autres termes, lorsque vous activez ce chiffrement, elle pas revenir en arrière et chiffrer les données qui existe déjà ; ni déchiffrera données hello qui existe déjà lorsque vous désactivez SSE.

Si vous souhaitez toouse cette fonctionnalité avec un compte de stockage classique, vous pouvez créer un nouveau compte de stockage du Gestionnaire de ressources et utiliser AzCopy toocopy hello données toohello nouveau compte.

### <a name="client-side-encryption"></a>chiffrement côté client
Nous l’avons mentionné chiffrement côté client de chiffrement hello de transfert de données hello. Cette fonctionnalité permet de vous tooprogrammatically chiffrer vos données dans une application cliente avant de l’envoyer sur toobe de câble hello écrite tooAzure stockage et tooprogrammatically déchiffrer vos données après l’avoir récupérée depuis le stockage Azure.

Cela ne permet pas le chiffrement en transit, mais il fournit également la fonctionnalité hello du chiffrement au repos. Notez que même si les données de salutation sont chiffrées en transit, nous vous recommandons toutefois à l’aide de parti de tootake HTTPS de vérifications d’intégrité de données intégré hello qui permettent de réduire les erreurs de réseau qui affectent l’intégrité de hello des données de hello.

Un exemple d’où vous pouvez l’utiliser est si vous possédez une application web qui stocke des objets BLOB et récupère des objets BLOB, et que vous souhaitez application hello et données toobe aussi sécurisées que possible. Dans ce cas, le chiffrement côté client est la méthode appropriée. le trafic de Hello entre les clients hello et hello Service Blob Azure contient les ressources hello chiffré et personne ne peut interpréter les données hello en transit et il reconstituer dans vos objets BLOB privé.

Le chiffrement côté client est intégré à hello Java et hello .NET bibliothèques clientes de stockage, qui à leur tour utilisent hello API de coffre de clé Azure, rendant assez facile pour vous tooimplement. Hello des processus de chiffrement et le déchiffrement des données de salutation utilise la technique d’enveloppe hello et stocke les métadonnées utilisées par le chiffrement hello dans chaque objet de stockage. Par exemple, pour les objets BLOB, il les stocke dans les métadonnées d’objets blob hello, tandis que pour les files d’attente, il ajoute message de file d’attente tooeach.

Pour le chiffrement hello lui-même, vous pouvez générer et gérer vos propres clés de chiffrement. Vous pouvez également utiliser des clés générées par hello bibliothèque cliente de stockage Azure, ou vous pouvez avoir hello Azure Key Vault générer des clés de hello. Vous pouvez stocker vos clés de chiffrement dans votre stockage de clés local, ou les stocker dans un coffre Azure Key Vault. Coffre de clés Azure vous permet de secrets de toohello toogrant accès les utilisateurs toospecific de coffre de clés Azure à l’aide d’Azure Active Directory. Cela signifie que non seulement pour toute personne peut lire hello Azure Key Vault et récupération des clés hello que vous utilisez pour le chiffrement côté client.

#### <a name="resources"></a>Ressources
* [Chiffrement et déchiffrement d’objets blob dans Microsoft Azure Storage à l'aide d'Azure Key Vault](storage-encrypt-decrypt-blobs-key-vault.md)

  Cet article explique comment le chiffrement côté client toouse avec Azure Key Vault, y compris comment toocreate hello de clés et les stocker dans le coffre de hello à l’aide de PowerShell.
* [Chiffrement côté client et Azure Key Vault pour Microsoft Azure Storage](storage-client-side-encryption.md)

  Cet article donne une explication du chiffrement côté client et fournit des exemples d’utilisation de hello client bibliothèque tooencrypt et decrypt ressources de stockage à partir des services de stockage de quatre hello. Il parle également d’Azure Key Vault.

### <a name="using-azure-disk-encryption-tooencrypt-disks-used-by-your-virtual-machines"></a>À l’aide du chiffrement de disque Azure tooencrypt disques utilisés par vos ordinateurs virtuels
Azure Disk Encryption est une nouvelle fonctionnalité. Cette fonctionnalité vous permet de disques de système d’exploitation tooencrypt hello et des disques de données utilisées par une Machine virtuelle de IaaS. Pour Windows, les lecteurs de hello sont chiffrés à l’aide de la technologie de chiffrement BitLocker standard. Pour Linux, les disques de hello sont chiffrées à l’aide de la technologie de hello DM-Crypt. Il est intégré à Azure Key Vault tooallow vous toocontrol et gérer des clés de chiffrement de disque hello.

solution de Hello prend en charge hello les scénarios suivants pour les machines virtuelles IaaS lorsqu’ils sont activés dans Microsoft Azure :

* Prise en main d’Azure Key Vault
* Machines virtuelles de niveau standard : [Machines virtuelles IaaS des séries A, D, DS, G, GS, etc.](https://azure.microsoft.com/pricing/details/virtual-machines/)
* Activation du chiffrement sur les machines virtuelles IaaS Windows et Linux
* Désactivation du chiffrement sur les systèmes d’exploitation et les lecteurs de données pour les machines virtuelles IaaS Windows
* Désactivation du chiffrement sur les lecteurs de données pour les machines virtuelles IaaS Linux
* Activation du chiffrement sur les machines virtuelles IaaS exécutant le système d’exploitation client Windows
* Activation du chiffrement sur les volumes avec chemins d’accès de montage
* Activation du chiffrement sur les machines virtuelles Linux configurées avec entrelacement de disques (RAID) à l’aide de mdadm
* Activation du chiffrement sur les machines virtuelles Linux à l’aide de LVM pour les disques de données
* Activation du chiffrement sur les machines virtuelles Windows configurées à l’aide d’espaces de stockage
* Toutes les régions publiques Azure sont prises en charge

solution de Hello ne prend pas en charge hello suivant la technologie de mise en production hello, fonctionnalités et scénarios :

* Machines virtuelles IaaS de niveau de base
* Désactivation du chiffrement sur un lecteur de système d’exploitation pour les machines virtuelles IaaS Linux
* Machines virtuelles IaaS qui sont créés à l’aide de la méthode de création VM hello classique
* Intégration à votre service de gestion de clés local
* Le stockage de fichiers Azure (système de partage de fichiers), NFS (Network File System), les volumes dynamiques et les machines virtuelles Windows configurées avec des systèmes RAID logiciels


> [!NOTE]
> Chiffrement de disque du système d’exploitation Linux est actuellement pris en charge sur hello suivant les distributions Linux : RHEL 7.2, CentOS 7.2n et Ubuntu 16.04.
>
>

Cette fonctionnalité garantit que toutes les données sur les disques de vos machines virtuelles sont chiffrées au repos dans Azure Storage.

#### <a name="resources"></a>les ressources
* [Chiffrement de disque Azure pour des machines virtuelles Windows et Linux IaaS](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption)

### <a name="comparison-of-azure-disk-encryption-sse-and-client-side-encryption"></a>Comparaison entre Azure Disk Encryption, SSE et le chiffrement côté client
#### <a name="iaas-vms-and-their-vhd-files"></a>Machines virtuelles IaaS et fichiers VHD associés
Pour les disques utilisés par des machines virtuelles IaaS, nous vous recommandons d’utiliser le chiffrement Azure Disk Encryption. Vous pouvez activer SSE tooencrypt hello fichiers VHD qui sont utilisé tooback ces disques dans le stockage Azure, mais il chiffre uniquement les données qui vient d’être écrites. Cela signifie que si vous créez une machine virtuelle et que vous activez SSE hello compte de stockage qui contient le fichier de disque dur virtuel hello, seules les modifications hello seront chiffrées, ne Hello pas de fichier de disque dur virtuel d’origine.

Si vous créez une machine virtuelle à l’aide d’une image à partir de hello Azure Marketplace, Azure effectue une [superficiellement copie](https://en.wikipedia.org/wiki/Object_copying) de hello image tooyour compte de stockage dans Azure Storage et il n’est pas chiffrée même si vous avez SSE activée. Après que qu’il crée la machine virtuelle de hello et démarre la mise à jour hello image, SSE démarrera le chiffrement des données de hello. Pour cette raison, il est meilleure toouse que chiffrement de disque Azure sur des machines virtuelles créé à partir d’images Bonjour Azure Marketplace si vous souhaitez les entièrement chiffré.

Si vous ajoutez une machine virtuelle déjà chiffrée dans Azure en local, vous être en mesure de tooupload hello chiffrement clés tooAzure le coffre de clés et continuer à utiliser le chiffrement hello pour cette machine virtuelle que vous utilisiez sur site. Chiffrement de disque Azure est activé toohandle ce scénario.

Si vous avez non chiffré de disque dur virtuel du site, vous pouvez la télécharger dans la galerie de hello comme une image personnalisée et configurer une machine virtuelle à partir de celui-ci. Dans ce cas à l’aide de modèles de gestionnaire de ressources hello, vous pouvez demander il tooturn sur le chiffrement des disques Azure lors de son démarrage à la machine virtuelle de hello.

Lorsque vous ajoutez un disque de données et montez sur hello machine virtuelle, vous pouvez activer le chiffrement des disques Azure sur ce disque de données. Il chiffre tout d’abord ce disque de données localement, et puis couche de gestion de service hello fera une écriture différée sur le stockage pour le contenu du stockage hello est chiffré.

#### <a name="client-side-encryption"></a>chiffrement côté client
Le chiffrement côté client est la méthode la plus sécurisée de chiffrement de vos données, car elle chiffre avant de transit et chiffre les données au repos hello hello. Cependant, il requiert que vous ajoutez à l’aide du stockage, vous ne voulez pas les applications de code tooyour toodo. Dans ce cas, vous pouvez utiliser HTTPs pour vos données en transit et les données de hello SSE tooencrypt au repos.

Le chiffrement côté client vous permet de chiffrer des entités de table, des messages de file d’attente et des objets blob. Avec SSE, vous ne pouvez chiffrer que des objets blob. Si vous avez besoin de table et la file d’attente toobe de données chiffrée, vous devez utiliser le chiffrement côté client.

Le chiffrement côté client est géré entièrement par l’application hello. C’est l’approche la plus sûre hello, mais effectue vous nécessitent l’application de tooyour toomake les modifications par programme et mettre le processus de gestion de clés en place. Vous pouvez utiliser cette lorsque vous souhaitez hello une sécurité supplémentaire au cours de transit et que vous souhaitez que votre toobe les données stockées chiffrée.

Chiffrement côté client est plus de charge sur le client de hello, et que tooaccount pour cela dans vos plans de l’évolutivité, en particulier si vous êtes chiffrer et transférer une grande quantité de données.

#### <a name="storage-service-encryption-sse"></a>Storage Service Encryption (SSE)
SSE est géré par le Stockage Azure. À l’aide d’instructions SSE ne fournit pas pour la sécurité de transfert de données hello hello, mais il chiffre les données de hello lorsqu’elles sont écrites tooAzure stockage. Il n’existe aucun impact sur les performances de hello lors de l’utilisation de cette fonctionnalité.

Avec SSE, vous pouvez uniquement chiffrer des objets blob de blocs, des objets blob d’ajout et des objets blob de pages. Si vous avez besoin des données de la table tooencrypt ou données de la file d’attente, vous devez envisager d’utiliser le chiffrement côté client.

Si vous avez une archive ou une bibliothèque de fichiers de disque dur virtuel que vous utilisez comme base pour la création d’ordinateurs virtuels, vous pouvez créer un nouveau compte de stockage, activer SSE et puis télécharger le compte de toothat de fichiers de disque dur virtuel hello. Ces fichiers VHD seront chiffrés par Azure Storage.

Si vous avez activé pour les disques hello dans une machine virtuelle et les instructions SSE activé sur le compte de stockage hello contenant les fichiers de disque dur virtuel hello un chiffrement de disque Azure, il fonctionne correctement ; Cela entraînerait des données qui vient d’être écrites en cours de chiffrement à deux reprises.

## <a name="storage-analytics"></a>Storage Analytics
### <a name="using-storage-analytics-toomonitor-authorization-type"></a>À l’aide du type de stockage Analytique toomonitor d’autorisation
Pour chaque compte de stockage, vous pouvez activer la journalisation de tooperform Analytique de stockage Azure et stocker des données de métriques. Il s’agit d’un toouse outil très utile lorsque vous souhaitez des métriques de performances hello toocheck d’un compte de stockage, ou que vous devez tootroubleshoot un compte de stockage, car vous avez des problèmes de performances.

Un autre élément de données, que vous pouvez voir dans les journaux d’analytique hello stockage est la méthode d’authentification hello utilisé par un utilisateur lors de l’accès au stockage. Par exemple, avec stockage d’objets Blob, vous pouvez voir s’ils utilisés d’une Signature d’accès partagé ou des clés de compte de stockage hello, ou si blob hello accessible a été publique.

Cela peut être très utile si vous sont protégeant étroitement les accès toostorage. Par exemple, dans le stockage Blob, vous pouvez définir toutes tooprivate de conteneurs hello et implémenter utilisez hello d’un service SAS dans l’ensemble de vos applications. Vous pouvez vérifier hello enregistre régulièrement toosee si vos objets BLOB est accessibles à l’aide de clés de compte de stockage hello, ce qui peuvent indiquer une violation de la sécurité, ou si les objets BLOB de hello sont publics, mais ils ne doivent pas être.

#### <a name="what-do-hello-logs-look-like"></a>Hello journaux l’aspect ?
Une fois que vous activez le compte hello storage metrics et journalisation via hello portail Azure, les données analytique démarrera tooaccumulate rapidement. enregistrement de Hello et les métriques pour chaque service est distinct ; journalisation de Hello est écrit uniquement les cas d’activité dans ce compte de stockage, alors que les métriques hello doivent être enregistrés pour toutes les minutes, toutes les heures ou tous les jours, en fonction de la configuration.

Hello journaux sont stockés dans les objets BLOB de blocs dans un conteneur nommé $logs hello compte de stockage. Ce conteneur est automatiquement créé quand Storage Analytics est activé. Une fois ce conteneur créé, vous ne pouvez pas le supprimer, même si vous pouvez en supprimer le contenu.

Sous le conteneur de hello $logs, il existe un dossier pour chaque service et des sous-dossiers pour hello année/mois/jour/heure. Sous les heures, les journaux de hello sont simplement numérotées. Il s’agit de quel hello structure du répertoire doit ressembler à :

![Affichage des fichiers journaux](./media/storage-security-guide/image1.png)

Chaque demande de tooAzure stockage est connecté. Voici une capture instantanée d’un fichier journal, montrant hello première assez de champs.

![Instantané d’un fichier journal](./media/storage-security-guide/image2.png)

Vous pouvez voir que vous pouvez utiliser hello journaux tootrack n’importe quel type de compte de stockage tooa appels.

#### <a name="what-are-all-of-those-fields-for"></a>À quoi servent tous ces champs ?
Il existe un article répertorié dans les ressources hello ci-dessous qui fournit liste hello Hello plusieurs champs dans les journaux hello et ils sont utilisés pour. Voici la liste hello des champs dans l’ordre :

![Instantané des champs d’un fichier journal](./media/storage-security-guide/image3.png)

Nous sommes intéressés par les entrées de hello pour GetBlob, et comment ils sont authentifiés, par conséquent, nous avons besoin toolook pour les entrées avec le type d’opération « Get-Blob » et vérifiez hello-état de la demande (4<sup>th</sup> colonne) et de type hello d’autorisation (8<sup>th</sup> colonne).

Par exemple, dans hello tout d’abord peu de lignes dans la liste hello ci-dessus, hello-état de la demande est « Success » et hello-type d’autorisation est « authenticated ». Cela signifie que la demande de hello a été validé à l’aide de la clé de compte de stockage hello.

#### <a name="how-are-my-blobs-being-authenticated"></a>Comment mes objets blob sont-ils authentifiés ?
Trois cas nous intéressent.

1. objet blob de Hello est public, et il est accessible à l’aide d’une URL sans une Signature d’accès partagé. Dans ce cas, hello-état de la demande est « AnonymousSuccess » et d’autorisation hello-type est « anonyme ».

   1.0;2015-11-17T02:01:29.0488963Z;GetBlob;**AnonymousSuccess**;200;124;37;**anonymous**;;mystorage…
2. objet blob de Hello est privé et a été utilisé avec une Signature d’accès partagé. Dans ce cas, hello-état de la demande est « SASSuccess » et d’autorisation hello-type est « sas ».

   1.0;2015-11-16T18:30:05.6556115Z;GetBlob;**SASSuccess**;200;416;64;**sas**;;mystorage…
3. objet blob de Hello est privé et clé de stockage hello a été utilisé tooaccess il. Dans ce cas, hello-état de la demande est «**réussite**« et est de type hello d’autorisation »**authentifié**».

   1.0;2015-11-16T18:32:24.3174537Z;GetBlob;**Success**;206;59;22;**authenticated**;mystorage…

Vous pouvez utiliser hello Microsoft Message Analyzer tooview et analyser ces journaux. Il inclue des fonctions de recherche et de filtre. Par exemple, vous pourriez toosearch pour les instances de toosee GetBlob si l’utilisation de hello est ce que vous attendez, c'est-à-dire les toomake que quelqu'un n’accède à votre compte de stockage inapproprié.

#### <a name="resources"></a>Ressources
* [Analyse du stockage](storage-analytics.md)

  Cet article est une vue d’ensemble de l’analytique de stockage et comment tooenable les.
* [Format du journal de l’analyse de stockage](https://msdn.microsoft.com/library/azure/hh343259.aspx)

  Cet article explique hello Format de journal Analytique de stockage et détails hello champs disponibles, y compris le type d’authentification, ce qui indique le type d’authentification utilisé pour la demande de hello de hello.
* [Surveillance d’un compte de stockage Bonjour portail Azure](storage-monitor-storage-account.md)

  Cet article explique comment tooconfigure analyse des métriques et la journalisation pour un compte de stockage.
* [Résolution des problèmes de bout en bout avec les métriques et la journalisation Azure, AzCopy et Message Analyzer](storage-e2e-troubleshooting.md)

  Cet article aborde le dépannage à l’aide de hello Analytique de stockage et montre comment toouse hello Microsoft Message Analyzer.
* [Microsoft Message Analyzer Operating Guide (Guide des opérations Microsoft Message Analyzer)](https://technet.microsoft.com/library/jj649776.aspx)

  Cet article est référence hello pour hello Microsoft Message Analyzer et inclut des liens tooa didacticiel, démarrage rapide et résumé des fonctionnalités.

## <a name="cross-origin-resource-sharing-cors"></a>Partage des ressources cross-origin (CORS)
### <a name="cross-domain-access-of-resources"></a>Accès interdomaines des ressources
Quand un navigateur web s’exécutant dans un domaine effectue une requête HTTP pour une ressource à partir d’un autre domaine, on parle de requête HTTP cross-origin. Par exemple, une page HTML traitée à partir de contoso.com effectue une requête pour une image jpeg hébergée sur fabrikam.blob.core.windows.net. Pour des raisons de sécurité, les navigateurs limitent les requêtes HTTP cross-origin lancées à partir de scripts, comme JavaScript. Cela signifie que, lorsque du code JavaScript dans une page web sur contoso.com demande que jpeg sur fabrikam.blob.core.windows.net, navigateur de hello ne permettre pas de demande de hello.

Ce que fait ce ont toodo avec le stockage Azure ? Ainsi, si vous stockez des éléments statiques tels que les fichiers de données JSON ou XML dans le stockage Blob à l’aide d’un compte de stockage nommé Fabrikam domaine hello pour les ressources de hello sera fabrikam.blob.core.windows.net et application web de contoso.com hello ne sera pas en mesure de tooaccess les à l’aide de JavaScript, car les domaines hello sont différents. Cela vaut également si vous essayez toocall d'entre hello des Services de stockage Azure – telles que le stockage de tables : qui retournent JSON toobe de données traitée par le client JavaScript de hello.

#### <a name="possible-solutions"></a>Solutions possibles
Une façon tooresolve il s’agit d’un domaine personnalisé, comme « storage.contoso.com » toofabrikam.blob.core.windows.net de tooassign. problème de Hello est que vous ne pouvez affecter ce compte de stockage tooone domaine personnalisé. Que se passe-t-il si les ressources de hello sont stockées dans plusieurs comptes de stockage ?

Une autre façon tooresolve il s’agit en tant que proxy pour les appels de stockage hello toohave hello web application act. Cela signifie que si vous téléchargez un fichier de tooBlob stockage, application web de hello serait soit écrire localement et copiez-le tooBlob stockage, soit il puis écrire tooBlob stockage et tous ses lues en mémoire. Ou bien, vous pouvez écrire une application web dédié (par exemple, une API Web) qui télécharge les fichiers hello localement et les écrit tooBlob stockage. Dans les deux cas, vous disposez tooaccount pour cette fonction déterminant l’évolutivité de hello a besoin.

#### <a name="how-can-cors-help"></a>En quoi CORS peut constituer une aide ?
Le stockage Azure vous permet de tooenable CORS – partage des ressources Cross-Origin. Pour chaque compte de stockage, vous pouvez spécifier les domaines qui peuvent accéder aux ressources hello dans ce compte de stockage. Par exemple, dans notre cas présentées ci-dessus, nous pouvons activer CORS sur le compte de stockage fabrikam.blob.core.windows.net hello et configurez-le tooallow accès toocontoso.com. Hello web application contoso.com peut accéder directement aux ressources hello dans fabrikam.blob.core.windows.net.

Une chose toonote est que CORS autorise l’accès, mais il ne fournit pas d’authentification, ce qui est nécessaire pour tous les accès non public des ressources de stockage. Cela signifie que vous pouvez uniquement accéder aux objets BLOB, si elles sont publiques ou vous inclure une Signature d’accès partagé vous donner la hello autorisation appropriée. Les tables, les files d’attente et les fichiers n’ont pas d’accès public et requièrent une SAP.

Par défaut, CORS est désactivé sur tous les services. Vous pouvez activer CORS à l’aide de hello API REST ou hello storage client library toocall une des stratégies de service hello méthodes tooset hello. Quand vous procédez ainsi, vous incluez une règle CORS, qui est au format XML. Voici un exemple d’une règle CORS qui a été définie avec l’opération Set Service Properties de hello pour hello Service Blob pour un compte de stockage. Vous pouvez effectuer cette opération à l’aide de la bibliothèque cliente de stockage hello ou hello API REST pour le stockage Azure.

```xml
<Cors>    
    <CorsRule>
        <AllowedOrigins>http://www.contoso.com, http://www.fabrikam.com</AllowedOrigins>
        <AllowedMethods>PUT,GET</AllowedMethods>
        <AllowedHeaders>x-ms-meta-data*,x-ms-meta-target*,x-ms-meta-abc</AllowedHeaders>
        <ExposedHeaders>x-ms-meta-*</ExposedHeaders>
        <MaxAgeInSeconds>200</MaxAgeInSeconds>
    </CorsRule>
<Cors>
```

Voici ce que signifie chaque ligne :

* **AllowedOrigins** en déduire les domaines de mise en correspondance peuvent demander et recevoir des données de service de stockage hello. Cela indique que contoso.com et fabrikam.com peuvent demander des données à partir de Blob Storage pour un compte de stockage spécifique. Vous pouvez également définir ce caractère générique tooa (\*) demandes de tous les domaines tooaccess tooallow.
* **AllowedMethods** liste hello des méthodes (verbes de requête HTTP) qui peut être utilisé lors de la demande de hello. Dans cet exemple, seuls PUT et GET sont autorisés. Vous pouvez définir ce caractère générique tooa (\*) tooallow toutes les méthodes toobe utilisé.
* **AllowedHeaders** il s’agit demande hello en-têtes hello du domaine d’origine peuvent spécifier lors de la demande de hello. Dans cet exemple, tous les en-têtes de métadonnées commençant par x-ms-meta-data, x-ms-meta-target et x-ms-meta-abc sont autorisés. Hello caractère générique (\*) indique que les en-têtes commençant par hello spécifié est autorisé.
* **ExposedHeaders** cela indique que les en-têtes de réponse doivent être exposées par l’émetteur de la demande hello navigateur toohello. Dans cet exemple, tout en-tête commençant par « x-ms - meta-» est exposé.
* **MaxAgeInSeconds** Voici hello durée maximale pendant laquelle un navigateur de cache demande OPTIONS préliminaire de hello. (Pour plus d’informations sur la demande préliminaire de hello, consultez le premier article hello ci-dessous.)

#### <a name="resources"></a>Ressources
Pour plus d’informations sur CORS et la manière dont tooenable, consultez ces ressources.

* [Prise en charge de partage de ressources Cross-Origin (CORS) pour hello des Services de stockage Azure sur Azure.com](storage-cors-support.md)

  Cet article fournit une vue d’ensemble de règles CORS et le fonctionnement des règles de tooset hello hello différents services de stockage.
* [Prise en charge de partage de ressources Cross-Origin (CORS) pour hello des Services de stockage Azure sur MSDN](https://msdn.microsoft.com/library/azure/dn535601.aspx)

  Il s’agit de documentation de référence de hello pour la prise en charge CORS pour les Services de stockage Azure hello. Cela a tooarticles liens application de service de stockage tooeach et présente un exemple et décrit chaque élément dans le fichier de règles CORS hello.
* [Microsoft Azure Storage: Introducing CORS (Microsoft Azure Storage : Présentation de CORS)](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/02/03/windows-azure-storage-introducing-cors.aspx)

  Il s’agit d’un lien toohello initiale l’article de blog annonce CORS et montrant comment toouse il.

## <a name="frequently-asked-questions-about-azure-storage-security"></a>Questions fréquemment posées (FAQ) sur la sécurité Azure Storage
1. **Comment puis-je vérifier l’intégrité de hello d’objets BLOB de hello que je suis transfert dans ou en dehors du stockage Azure si je ne parviens pas à utiliser le protocole HTTPS hello ?**

   Si pour une raison quelconque, vous devez toouse HTTP au lieu de HTTPS et que vous travaillez avec des objets BLOB de blocs, vous pouvez utiliser la vérification de MD5 toohelp vérifier l’intégrité de hello d’objets BLOB de hello en cours de transfert. Ceci contribuera à la protection contre les erreurs au niveau du réseau/transport, mais pas nécessairement contre les attaques intermédiaires.

   Si vous pouvez utiliser le protocole HTTPS, qui fournit une sécurité au niveau du transport, alors l’utilisation de la vérification MD5 est redondant et inutile.

   Pour plus d’informations, consultez hello [vue d’ensemble du MD5 Azure Blob](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/02/18/windows-azure-blob-md5-overview.aspx).
2. **Qu’en est-il de la compatibilité FIPS pour les États-Unis de hello américain ?**

   Hello United States traitement Standard FIPS (Federal Information) définit les algorithmes de chiffrement approuvés pour une utilisation par des États-Unis Systèmes informatiques de gouvernement fédéral pour la protection de hello des données sensibles. L’activation de FIPS mode sur un serveur Windows ou le bureau indique hello du système d’exploitation que les algorithmes de chiffrement validés FIPS uniquement doivent être utilisés. Si une application utilise des algorithmes non conformes, les applications hello seront arrêtera. Les versions avec.NET Framework 4.5.2 ou une version ultérieure, application hello change automatiquement algorithmes de toouse compatibles FIPS d’algorithmes de chiffrement hello lorsque l’ordinateur de hello est en mode FIPS.

   Microsoft laisse des tooeach client toodecide indique si le mode FIPS tooenable. Nous pensons qu’il n’existe aucune raison incontournable pour les clients qui ne sont pas sujet toogovernment réglementations tooenable FIPS en mode par défaut.

   **Ressources**

* [Why We’re Not Recommending “FIPS Mode” Anymore (Pourquoi nous ne recommandons plus le « mode FIPS »)](http://blogs.technet.com/b/secguide/archive/2014/04/07/why-we-re-not-recommending-fips-mode-anymore.aspx)

  Cet article de blog donne une vue d’ensemble des normes FIPS et explique pourquoi le mode FIPS n’est plus activé par défaut.
* [FIPS 140 Validation (Validation de la norme FIPS 140)](https://technet.microsoft.com/library/cc750357.aspx)

  Cet article fournit des informations sur comment produits Microsoft et des modules de chiffrement est compatible avec la norme FIPS de hello des hello US américain.
* [Effets des paramètres de sécurité « Chiffrement système : utilisez des algorithmes compatibles FIPS pour le chiffrement, le hachage et la signature » dans Windows XP et les versions ultérieures de Windows](https://support.microsoft.com/kb/811833)

  Cet article traite d’utiliser le mode FIPS dans les anciens ordinateurs Windows hello.
