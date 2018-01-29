---
title: "Vue d’ensemble de la sécurité dans Data Lake Store | Microsoft Docs"
description: "Comprendre en quoi Azure Data Lake Store est un magasin de Big Data plus sécurisé"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ebd5b2ac-c5cc-46d4-9cfd-1a1ee70024c2
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 11/28/2017
ms.author: nitinme
ms.openlocfilehash: 52e176711f512e8a3788309a58011c8484821a1e
ms.sourcegitcommit: cf42a5fc01e19c46d24b3206c09ba3b01348966f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/29/2017
---
# <a name="security-in-azure-data-lake-store"></a>Sécurité dans Azure Data Lake Store
Un grand nombre d’entreprises tirent parti de l’analyse du Big Data pour bénéficier d’informations métier afin de prendre des décisions éclairées. Une organisation peut évoluer dans un environnement complexe et réglementé, avec un nombre croissant d’utilisateurs divers. Il est essentiel pour une entreprise de garantir que les données métier critiques sont stockées de manière plus sécurisée, avec le niveau d’accès adéquat pour chaque utilisateur. Azure Data Lake Store vous permet de respecter ces exigences de sécurité. Dans cet article, découvrez les fonctionnalités de sécurité de Data Lake Store, notamment :

* Authentification
* Autorisation
* Isolement réseau
* Protection des données
* Audit

## <a name="authentication-and-identity-management"></a>Authentification et gestion des identités
L’authentification est le processus par lequel l’identité d’un utilisateur est vérifiée lorsque celui-ci interagit avec Data Lake Store ou tout service qui se connecte à Data Lake Store. Pour l’authentification et la gestion des identités, Data Lake Store utilise [Azure Active Directory](../active-directory/active-directory-whatis.md), une solution complète pour la gestion des identités et des accès dans le cloud qui simplifie la gestion des utilisateurs et des groupes.

Chaque abonnement Azure peut être associé à une instance d’Azure Active Directory. Seuls les utilisateurs et les identités de service qui sont définis dans votre service Azure Active Directory peuvent accéder à votre compte Data Lake Store, à l’aide du portail Azure, des outils de ligne de commande, ou via les applications clientes que votre organisation crée avec le kit de développement logiciel (SDK) Azure Data Lake Store. Les principaux avantages de l’utilisation d’Azure Active Directory en tant que mécanisme de contrôle d’accès centralisé sont les suivants :

* Gestion du cycle de vie des identités simplifiée. L’identité d’un utilisateur ou d’un service (une identité de principal du service) peut être rapidement créée et révoquée en supprimant ou en désactivant simplement le compte dans le répertoire.
* Authentification multifacteur [L’authentification multifacteur](../multi-factor-authentication/multi-factor-authentication.md) fournit une couche supplémentaire de sécurité pour les connexions et les transactions utilisateur.
* Authentification à partir de n’importe quel client via un protocole ouvert standard, tel qu’OAuth ou OpenID.
* Fédération avec les services de répertoire d’entreprise et les fournisseurs d’identité cloud.

## <a name="authorization-and-access-control"></a>Autorisation et contrôle d’accès
Une fois qu’un utilisateur est authentifié par Azure Active Directory pour accéder à Azure Data Lake Store, les contrôles d’autorisation accèdent aux autorisations pour Data Lake Store. Data Lake Store sépare l’autorisation pour les activités relatives aux comptes et aux données de la manière suivante :

* [Le contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-what-is.md) (RBAC) fournit par Azure pour la gestion des comptes ;
* ACL POSIX pour accéder aux données dans le magasin

### <a name="rbac-for-account-management"></a>RBAC pour la gestion des comptes
Par défaut, quatre rôles de base sont définis pour Data Lake Store. Les rôles permettent d’exécuter différentes opérations sur un compte Data Lake Store via le portail Azure, les applets de commande PowerShell et les API REST. Les rôles Propriétaire et Collaborateur peuvent effectuer un large éventail de fonctions d’administration sur le compte. Vous pouvez affecter le rôle Lecteur aux utilisateurs qui interagissent uniquement avec les données.

![Rôles RBAC](./media/data-lake-store-security-overview/rbac-roles.png "Rôles RBAC")

Notez que, même si les rôles sont attribués pour la gestion des comptes, certains rôles affectent l’accès aux données. Vous devez utiliser les ACL pour contrôler l’accès aux opérations qu’un utilisateur peut effectuer sur le système de fichiers. Le tableau suivant présente un résumé des droits d’accès aux données et aux droits de gestion pour les rôles par défaut.

| contrôleur | Droits de gestion | Droits d’accès aux données | Explication |
| --- | --- | --- | --- |
| Aucun rôle affecté |Aucun |Régi par ACL |L’utilisateur ne peut pas utiliser le portail Azure ou les applets de commande Azure PowerShell pour parcourir Data Lake Store. L’utilisateur peut uniquement utiliser les outils de ligne de commande. |
| Propriétaire |Tout |Tout |Le rôle Propriétaire est un super utilisateur. Ce rôle peut tout gérer et bénéficie d’un accès total aux données. |
| Lecteur |Lecture seule |Régi par ACL |Le rôle Lecteur peut tout afficher en matière de gestion des comptes, notamment quel utilisateur est affecté à quel rôle. Le rôle Lecteur ne permet pas d’effectuer des modifications. |
| Collaborateur |Tout, sauf ajouter et supprimer des rôles |Régi par ACL |Le rôle Collaborateur peut gérer certains aspects d’un compte, tels que les déploiements et la création et la gestion des alertes. Le rôle Collaborateur ne peut pas ajouter ou supprimer des rôles. |
| Administrateur de l'accès utilisateur |Ajouter et supprimer des rôles |Régi par ACL |Le rôle Administrateur de l’accès utilisateur peut gérer l’accès des utilisateurs aux comptes. |

Pour obtenir des instructions, consultez [Affecter les utilisateurs ou les groupes de sécurité aux comptes Azure Data Lake Store](data-lake-store-secure-data.md#assign-users-or-security-groups-to-azure-data-lake-store-accounts).

### <a name="using-acls-for-operations-on-file-systems"></a>Utilisation des ACL pour les opérations sur les systèmes de fichiers
Data Lake Store est un système de fichiers hiérarchique comme Hadoop HDFS Distributed File System (HDFS), et il prend en charge les [ACL POSIX](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Elle contrôle la lecture (r), l’écriture (w) et exécute(x) les autorisations des ressources pour le rôle Propriétaire, le groupe Propriétaires et d’autres utilisateurs et groupes. Dans la version publique préliminaire de Data Lake Store (la version actuelle), les ACL peuvent être activées au niveau du dossier racine, des sous-dossiers et des fichiers individuels. Pour plus d’informations sur le fonctionnement des ACL dans le contexte de Data Lake Store, consultez [Contrôle d’accès dans Data Lake Store](data-lake-store-access-control.md).

Nous vous recommandons de définir des ACL pour plusieurs utilisateurs à l’aide des [groupes de sécurité](../active-directory/active-directory-groups-create-azure-portal.md). Ajoutez des utilisateurs dans un groupe de sécurité, puis affectez les ACL d’un fichier ou dossier à ce groupe de sécurité. Cela est utile lorsque vous souhaitez fournir un accès personnalisé, car vous êtes limité à l’ajout de neuf entrées maximum pour un accès personnalisé. Pour plus d’informations sur comment améliorer la sécurisation des données stockées dans Data Lake Store à l’aide de groupes de sécurité Azure Active Directory, consultez [Affecter des utilisateurs ou un groupe de sécurité comme ACL au système de fichiers Azure Data Lake Store](data-lake-store-secure-data.md#filepermissions).

![Lister les accès standard et personnalisés](./media/data-lake-store-security-overview/adl.acl.2.png "Lister les accès standard et personnalisés")

## <a name="network-isolation"></a>Isolement réseau
Utilisez Data Lake Store pour contrôler l’accès à votre magasin de données au niveau du réseau. Vous pouvez activer des pare-feu et définir une plage d’adresses IP pour vos clients approuvés. Avec une plage d’adresses IP, seuls les clients qui ont une adresse IP dans la plage définie peuvent se connecter à Data Lake Store.

![Paramètres de pare-feu et accès IP](./media/data-lake-store-security-overview/firewall-ip-access.png "Paramètres de pare-feu et accès IP")

## <a name="data-protection"></a>Protection des données
Azure Data Lake Store protège vos données tout au long de leur cycle de vie. Pour les données en transit, Data Lake Store utilise le protocole normalisé TLS (Transport Layer Security) pour sécuriser les données sur le réseau.

![Chiffrement dans Data Lake Store](./media/data-lake-store-security-overview/adls-encryption.png "Chiffrement dans Data Lake Store")

Data Lake Store fournit également le chiffrement des données stockées dans le compte. Vous pouvez choisir de chiffrer vos données ou non. Si vous optez pour le chiffrement, les données stockées dans Data Lake Store sont chiffrées avant d’être stockées sur un support permanent. Dans ce cas, Data Lake Store chiffre automatiquement les données avant qu’elles soient rendues persistantes et les déchiffre avant qu’elles soient récupérées ; ainsi, ces opérations sont totalement transparentes vis-à-vis du client qui accède aux données. Aucune modification de code n’est nécessaire côté client pour chiffrer/déchiffrer les données.

Concernant la gestion des clés, Data Lake Store met à votre disposition deux modes pour gérer les clés de chiffrement principales, qui sont nécessaires pour déchiffrer les données stockées dans le Data Lake Store. Vous pouvez soit laisser Data Lake Store gérer les clés de chiffrement principales, soit choisir de conserver la propriété des clés de chiffrement principales en utilisant votre compte Azure Key Vault. Vous spécifiez le mode de gestion de clés durant la création d’un compte Data Lake Store. Pour savoir comment fournir une configuration avec chiffrement, consultez [Prise en main d’Azure Data Lake Store à l’aide du Portail Azure](data-lake-store-get-started-portal.md).

## <a name="auditing-and-diagnostic-logs"></a>Journaux d’audit et de diagnostic
Vous pouvez utiliser les journaux d’audit ou de diagnostic selon si vous recherchez des journaux sur des activités liées à la gestion ou des activités liées aux données.

* Les activités liées à la gestion utilisent les API d’Azure Resource Manager et sont affichées dans le portail Azure via les journaux d’audit.
* Les activités liées aux données utilisent les API REST WebHDFS et sont affichées dans le portail via les journaux de diagnostic.

### <a name="auditing-logs"></a>Journaux d’audit
Pour respecter les réglementations, une organisation peut avoir besoin de pistes d’audit adéquates si elle doit examiner en profondeur des incidents spécifiques. Data Lake Store est doté de fonctionnalités intégrées de surveillance et d’audit et journalise toutes les activités de gestion des comptes.

Pour les pistes d’audit de gestion des comptes, affichez et choisissez les colonnes que vous souhaitez journaliser. Vous pouvez également exporter des journaux d’audit vers Azure Storage.

![Journaux d’audit](./media/data-lake-store-security-overview/audit-logs.png "Journaux d’Audit")

### <a name="diagnostic-logs"></a>Journaux de diagnostic
Vous pouvez définir les pistes d’audit d’accès aux données dans le portail Azure (dans Paramètres de diagnostic) et créer un compte Azure Blob Storage dans lequel les journaux sont stockés.

![Journaux de diagnostic](./media/data-lake-store-security-overview/diagnostic-logs.png "Journaux de diagnostic")

Après avoir configuré les paramètres de diagnostic, vous pouvez afficher les journaux dans l’onglet **Journaux de diagnostic** .

Pour plus d’informations sur l’utilisation des journaux de diagnostic avec Azure Data Lake Store, consultez [Accès aux journaux de diagnostic d’Azure Data Lake Store](data-lake-store-diagnostic-logs.md).

## <a name="summary"></a>Résumé
Les clients professionnels exigent une plateforme cloud d’analyse des données sécurisée et facile à utiliser. Azure Data Lake Store est conçu pour répondre à ces exigences avec la gestion des identités et l’authentification via l’intégration d’Azure Active Directory, l’autorisation basée sur les ACL, l’isolement réseau, le chiffrement des données en transit et au repos (à venir) et l’audit.

Si vous souhaitez voir de nouvelles fonctionnalités de Data Lake Store, envoyez-nous vos commentaires sur notre [forum UserVoice Data Lake Store](https://feedback.azure.com/forums/327234-data-lake).

## <a name="see-also"></a>Voir aussi
* [Présentation d’Azure Data Lake Store](data-lake-store-overview.md)
* [Prise en main d’Azure Data Lake Store avec le portail Azure](data-lake-store-get-started-portal.md)
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)

