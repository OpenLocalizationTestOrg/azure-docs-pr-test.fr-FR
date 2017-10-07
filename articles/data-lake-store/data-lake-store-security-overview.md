---
title: "aaaOverview de la sécurité dans Data Lake Store | Documents Microsoft"
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
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 69e20bd046a9427202074baf59bff13f5b6a83ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="security-in-azure-data-lake-store"></a>Sécurité dans Azure Data Lake Store
De nombreuses entreprises Tirez profit de l’analytique des données volumineuses pour business toohelp d’insights que les rendre actives décisions. Une organisation peut évoluer dans un environnement complexe et réglementé, avec un nombre croissant d’utilisateurs divers. Il est essentiel pour une entreprise toomake assurer que les données critiques sont stockées en toute sécurité, avec le niveau approprié de hello d’accès accordé aux utilisateurs de tooindividual. Azure Data Lake Store est conçu toohelp respecter ces exigences de sécurité. Dans cet article, Découvrez les fonctionnalités de sécurité hello Lake du magasin de données, y compris :

* Authentification
* Autorisation
* Isolement réseau
* Protection des données
* Audit

## <a name="authentication-and-identity-management"></a>Authentification et gestion des identités
L’authentification consiste à hello par lequel l’identité d’un utilisateur est vérifiée lorsque l’utilisateur de hello interagit avec Data Lake Store ou tout service qui se connecte tooData Lake Store. Pour l’authentification et de gestion des identités, Data Lake Store utilise [Azure Active Directory](../active-directory/active-directory-whatis.md), une identité et accès management solution cloud complète qui simplifie la gestion des utilisateurs et groupes hello.

Chaque abonnement Azure peut être associé à une instance d’Azure Active Directory. Seuls les utilisateurs et les identités de service qui sont définies dans votre service Azure Active Directory peuvent accéder à votre compte Data Lake Store, à l’aide de hello portail Azure, les outils de ligne de commande, ou via des applications client que génère de votre organisation à l’aide de hello Azure Data Kit de développement logiciel Lake Store. Les principaux avantages de l’utilisation d’Azure Active Directory en tant que mécanisme de contrôle d’accès centralisé sont les suivants :

* Gestion du cycle de vie des identités simplifiée. identité Hello d’un utilisateur ou un service (une identité principale du service) peut être rapidement créée et rapidement révoquée par simplement la suppression ou la désactivation du compte hello dans le répertoire de hello.
* Authentification multifacteur [L’authentification multifacteur](../multi-factor-authentication/multi-factor-authentication.md) fournit une couche supplémentaire de sécurité pour les connexions et les transactions utilisateur.
* Authentification à partir de n’importe quel client via un protocole ouvert standard, tel qu’OAuth ou OpenID.
* Fédération avec les services de répertoire d’entreprise et les fournisseurs d’identité cloud.

## <a name="authorization-and-access-control"></a>Autorisation et contrôle d’accès
Une fois Azure Active Directory authentifie un utilisateur afin que hello utilisateur peut accéder à Azure Data Lake Store, contrôles d’autorisation d’accès nécessaires pour Data Lake Store. Data Lake Store sépare d’autorisation pour les activités relatives aux comptes et liées aux données Bonjour suivant de manière :

* [Le contrôle d’accès en fonction du rôle](../active-directory/role-based-access-control-what-is.md) (RBAC) fournit par Azure pour la gestion des comptes ;
* POSIX ACL pour l’accès aux données dans le magasin de hello

### <a name="rbac-for-account-management"></a>RBAC pour la gestion des comptes
Par défaut, quatre rôles de base sont définis pour Data Lake Store. les rôles Hello autorisent différentes opérations sur un compte Data Lake Store via hello portail Azure, les applets de commande PowerShell et les API REST. Hello propriétaire et les rôles de collaborateur peuvent effectuer diverses fonctions d’administration sur le compte de hello. Vous pouvez affecter toousers de rôle de lecteur hello qui peuvent interagir uniquement avec les données.

![Rôles RBAC](./media/data-lake-store-security-overview/rbac-roles.png "Rôles RBAC")

Notez que, bien que les rôles sont attribués pour la gestion de compte, certains rôles affectent toodata d’accès. Vous devez toouse ACL toocontrol accès toooperations qu’un utilisateur peut effectuer sur le système de fichiers hello. Hello tableau suivant montre un résumé des droits et de gestion des droits d’accès pour hello rôles par défaut.

| contrôleur | Droits de gestion | Droits d’accès aux données | Explication |
| --- | --- | --- | --- |
| Aucun rôle affecté |Aucun |Régi par ACL |utilisateur de Hello ne peut pas utiliser hello Azure portal ou Azure PowerShell cmdlets toobrowse Data Lake Store. utilisateur de Hello peut utiliser des outils de ligne de commande uniquement. |
| Propriétaire |Tout |Tout |rôle de propriétaire Hello est un super utilisateur. Ce rôle peut tout gérer et a un accès complet toodata. |
| Lecteur |Lecture seule |Régi par ACL |rôle de lecteur Hello peut tout afficher concernant la gestion des comptes, par exemple quels utilisateur rôle toowhich. rôle de lecteur Hello ne peut pas apporter des modifications. |
| Collaborateur |Tout, sauf ajouter et supprimer des rôles |Régi par ACL |rôle de collaborateur Hello peut gérer certains aspects d’un compte, tels que les déploiements et la création et la gestion des alertes. rôle de collaborateur Hello ne peut pas ajouter ou supprimer des rôles. |
| Administrateur de l'accès utilisateur |Ajouter et supprimer des rôles |Régi par ACL |rôle d’administrateur de l’accès utilisateur Hello peut gérer tooaccounts des accès utilisateur. |

Pour obtenir des instructions, consultez [affecter des utilisateurs ou des groupes de sécurité des comptes de tooData Lake Store](data-lake-store-secure-data.md#assign-users-or-security-groups-to-azure-data-lake-store-accounts).

### <a name="using-acls-for-operations-on-file-systems"></a>Utilisation des ACL pour les opérations sur les systèmes de fichiers
Data Lake Store est un système de fichiers hiérarchique comme Hadoop HDFS Distributed File System (HDFS), et il prend en charge les [ACL POSIX](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsPermissionsGuide.html#ACLs_Access_Control_Lists). Elle contrôle en lecture (r), écriture (w) et exécuter (tooresources d’autorisations pour le rôle de propriétaire hello, pour le groupe de propriétaires hello et pour d’autres utilisateurs et groupes x). Bonjour Data Lake Store Public Preview (version actuelle de hello), les ACL peuvent être activées sur le dossier racine de hello, dans les sous-dossiers et sur des fichiers individuels. Pour plus d’informations sur le fonctionnement des ACL dans le contexte de Data Lake Store, consultez [Contrôle d’accès dans Data Lake Store](data-lake-store-access-control.md).

Nous vous recommandons de définir des ACL pour plusieurs utilisateurs à l’aide des [groupes de sécurité](../active-directory/active-directory-accessmanagement-manage-groups.md). Ajouter le groupe de sécurité utilisateurs tooa, puis attribuez les ACL hello pour un groupe de sécurité toothat fichier ou dossier. Cela est utile lorsque vous souhaitez que les accès personnalisé tooprovide, car vous êtes limité tooadding un maximum de neuf entrées pour un accès personnalisé. Pour plus d’informations sur la façon dont les toobetter sécuriser les données stockées dans Data Lake Store à l’aide de groupes de sécurité Azure Active Directory, consultez [affecter des utilisateurs ou groupe de sécurité comme les ACL toohello système de fichiers Azure Data Lake Store](data-lake-store-secure-data.md#filepermissions).

![Lister les accès standard et personnalisés](./media/data-lake-store-security-overview/adl.acl.2.png "Lister les accès standard et personnalisés")

## <a name="network-isolation"></a>Isolement réseau
Stocker des données tooyour d’utilisez Data Lake Store toohelp contrôle l’accès au niveau du réseau hello. Vous pouvez activer des pare-feu et définir une plage d’adresses IP pour vos clients approuvés. Une plage d’adresses IP, seuls les clients qui ont une adresse IP au sein de la plage de hello défini peuvent se connecter tooData Lake Store.

![Paramètres de pare-feu et accès IP](./media/data-lake-store-security-overview/firewall-ip-access.png "Paramètres de pare-feu et accès IP")

## <a name="data-protection"></a>Protection des données
Azure Data Lake Store protège vos données tout au long de leur cycle de vie. Pour les données en transit, Data Lake Store utilise les données toosecure du protocole de sécurité TLS (Transport Layer) hello normalisées réseau hello.

![Chiffrement dans Data Lake Store](./media/data-lake-store-security-overview/adls-encryption.png "Chiffrement dans Data Lake Store")

Data Lake Store fournit également le chiffrement de données qui sont stockés dans le compte de hello. Vous pouvez choisir toohave vos données chiffrées ou optez pour aucun chiffrement. Si vous choisissez cette option pour le chiffrement, les données stockées dans Data Lake Store sont chiffrée toostoring préalable sur un support permanent. Dans ce cas, Data Lake Store toopersisting préalable des données de chiffre et déchiffre tooretrieval préalable de données, afin qu’il soit client toohello totalement transparente l’accès aux données de hello automatiquement. Il n’existe aucune modification du code requise sur les données hello client côté tooencrypt/decrypt.

Gestion de clés, Data Lake Store propose deux modes de gestion de vos clés de chiffrement principale (MEKs), qui sont requis pour le déchiffrement des données qui sont stockées dans hello Data Lake Store. Vous pouvez laisser Data Lake Store gérer hello MEKs pour vous, ou choisissez tooretain approprier MEKs hello à l’aide de votre compte Azure Key Vault. Vous spécifiez le mode de gestion de clés hello tandis que lors de la création d’un compte Data Lake Store. Pour plus d’informations sur la façon de configuration relatives au chiffrement de tooprovide, consultez [prise en main Azure Data Lake Store à l’aide de hello Azure Portal](data-lake-store-get-started-portal.md).

## <a name="auditing-and-diagnostic-logs"></a>Journaux d’audit et de diagnostic
Vous pouvez utiliser les journaux d’audit ou de diagnostic selon si vous recherchez des journaux sur des activités liées à la gestion ou des activités liées aux données.

* Activités de gestion utilisent les API du Gestionnaire de ressources Azure et sont signalées dans hello portail Azure via les journaux d’audit.
* Les activités liées aux données utilisent les API REST de WebHDFS et sont signalées dans hello portail Azure via les journaux de diagnostic.

### <a name="auditing-logs"></a>Journaux d’audit
toocomply avec les réglementations, une organisation peut nécessiter des pistes d’audit appropriées si elle a besoin toodig dans des incidents spécifiques. Data Lake Store est doté de fonctionnalités intégrées de surveillance et d’audit et journalise toutes les activités de gestion des comptes.

Compte gestion des journaux d’audit, afficher et sélectionner des colonnes de hello que vous souhaitez toolog. Vous pouvez également exporter tooAzure de journaux d’audit stockage.

![Journaux d’audit](./media/data-lake-store-security-overview/audit-logs.png "Journaux d’Audit")

### <a name="diagnostic-logs"></a>Journaux de diagnostic
Vous pouvez définir des pistes d’audit de l’accès aux données dans le portail Azure (dans les paramètres de Diagnostic) de hello et créer un compte de stockage d’objets Blob Azure sur lequel sont enregistrés les journaux de hello.

![Journaux de diagnostic](./media/data-lake-store-security-overview/diagnostic-logs.png "Journaux de diagnostic")

Après avoir configuré les paramètres de diagnostic, vous pouvez afficher des journaux de hello sur hello **journaux de Diagnostic** onglet.

Pour plus d’informations sur l’utilisation des journaux de diagnostic avec Azure Data Lake Store, consultez [Accès aux journaux de diagnostic d’Azure Data Lake Store](data-lake-store-diagnostic-logs.md).

## <a name="summary"></a>Résumé
Les clients d’entreprise exigent une plateforme cloud données analytique est toouse simple et sécurisée. Azure Data Lake Store est conçu toohelp surmonter ces difficultés via la gestion des identités et l’authentification via l’intégration d’Azure Active Directory, d’autorisation basée sur les ACL, l’isolement réseau, le chiffrement des données en transit et au repos (entrants hello ultérieures) et l’audit.

Si vous souhaitez toosee les nouvelles fonctionnalités de Data Lake Store, nous envoyer vos commentaires Bonjour [UserVoice de magasin de données Lake forum](https://feedback.azure.com/forums/327234-data-lake).

## <a name="see-also"></a>Voir aussi
* [Présentation d’Azure Data Lake Store](data-lake-store-overview.md)
* [Prise en main d’Azure Data Lake Store avec le portail Azure](data-lake-store-get-started-portal.md)
* [Sécuriser les données dans Data Lake Store](data-lake-store-secure-data.md)

