---
title: "Modèle d’Application Web locataire aaaMulti | Documents Microsoft"
description: "Recherchez des présentations architecturales et des modèles de conception qui décrivent comment tooimplement mutualisée web d’application dans Azure."
services: 
documentationcenter: .net
author: wadepickett
manager: wpickett
editor: 
ms.assetid: 4f0281d2-1555-42b0-a99d-1222fade0b0f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/05/2015
ms.author: wpickett
ms.openlocfilehash: 3b7822c8ca4aa50d295a174973ae4746c230ba66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="multitenant-applications-in-azure"></a>Applications mutualisées dans Azure
Une application multi-locataire est une ressource partagée qui permet les utilisateurs ou les « clients », tooview hello application distincte comme s’il s’agissait leur propres. Un scénario typique qui se prête à une application multi-locataire tooa est un dans lequel tous les utilisateurs de hello application peut-être souhaitez l’expérience utilisateur toocustomize hello mais sinon hello les mêmes exigences commerciales de base. Exemples d'applications mutualisées : Office 365, Outlook.com et visualstudio.com.

Du point de vue d’un fournisseur d’application, les avantages de hello de l’architecture mutualisée principalement liés toooperational et rentabilité. Une version de votre application peut répondre aux besoins de hello de nombreux clients/client, ce qui permet la consolidation du système des tâches d’administration telles que la surveillance, réglage des performances, une maintenance logicielle et les sauvegardes de données.

suivant de Hello fournit une liste des objectifs plus significatifs de hello et les exigences du point de vue d’un fournisseur.

* **Approvisionnement**: vous devez être en mesure de tooprovision de nouveaux clients pour l’application hello.  Pour les applications multi-locataires avec un grand nombre de clients, il est généralement nécessaire tooautomate ce processus par activation de l’approvisionnement de libre-service.
* **Facilité de maintenance**: vous devez être en mesure de tooupgrade hello application et effectuer d’autres tâches de maintenance lorsque plusieurs clients l’utilisent.
* **Analyse**: vous doit être application hello toomonitor en mesure de toutes les heures tooidentify tous les problèmes et tootroubleshoot les. Cela inclut l’analyse comment chaque client est à l’aide d’application hello.

Une application mutualisée correctement implémentée fournit suivant de hello avantages toousers.

* **Isolation**: activités hello de clients individuels n’affectent pas les utiliser hello application hello par d’autres clients. Les locataires ne peuvent pas accéder aux données des uns et des autres. Il s’affiche toohello client comme s’ils ont une utilisation exclusive de l’application hello.
* **Disponibilité**: les locataires individuels souhaitez toobe d’application hello constamment disponible, peut-être avec garanties définies dans un contrat SLA. Là encore, les activités hello d’autres locataires ne devraient pas affecter disponibilité hello de l’application hello.
* **Évolutivité**: application hello s’adapte à la demande de hello toomeet de clients individuels. Hello présence et les actions d’autres locataires n’affecte pas les performances de hello d’application hello.
* **Les coûts**: les coûts sont inférieurs à une application dédiée à locataire unique en cours d’exécution, car une architecture mutualisée permet hello partage des ressources.
* **Possibilités de personnalisation**. application de hello toocustomize Hello possibilité pour un locataire de différentes manières, telles que l’ajout ou suppression de fonctionnalités, modification des couleurs et les logos ou même ajouter leur propre code ou un script.

En bref, lorsqu’il y a plusieurs considérations que vous devez prendre en compte tooprovide un service hautement évolutif, il existe également un nombre d’objectifs de hello et exigences des applications mutualisées réduire courantes. Certains ne soient pas pertinentes dans des scénarios spécifiques et l’importance de hello des objectifs individuels et spécifications varient dans chaque scénario. En tant que fournisseur d’application mutualisé hello, vous devez également des objectifs et exigences comme clients hello objectifs et exigences, rentabilité, facturation, plusieurs niveaux de service, l’approvisionnement, l’analyse de la facilité de maintenance et l’automatisation de la réunion.

Pour plus d'informations sur les considérations supplémentaires d'une application mutualisée en matière de conception, consultez la page [Hébergement d'une application mutualisée dans Azure][Hosting a Multi-Tenant Application on Azure]. Pour plus d’informations sur les modèles d’architecture de données des applications de base de données de logiciels en tant que service (SaaS) mutualisés, consultez [Modèles de conception pour les applications SaaS mutualisées avec Base de données SQL Azure](sql-database/sql-database-design-patterns-multi-tenancy-saas-applications.md). 

Azure fournit de nombreuses fonctionnalités qui vous permettent de tooaddress hello principaux problèmes rencontrés lors de la conception d’un système multi-locataire.

**Isolement**

* Segmentation des locataires de site web en fonction des en-têtes d'hôte avec ou sans communication SSL
* Segmentation des locataires de site web en fonction des paramètres de requête
* Services Web dans les rôles de travail
  * Rôles de travail. en général, traitent les données back-end hello d’une application.
  * Rôles Web qui agissent en tant que serveur frontal de hello pour les applications.

**Stockage**

Gestion des données telles que les services de base de données SQL Azure ou le stockage Azure telles que hello service qui fournit des services pour le stockage de grandes quantités de données non structurées de Table et hello service d’objets Blob qui fournit des services toostore grandes quantités de texte non structuré ou données binaires telles que la vidéo, audio et images.

* Sécurisation de données mutualisées dans des connexions SQL Server par locataire appropriées de la base de données SQL.
* À l’aide de Tables Azure pour l’Application de ressources en spécifiant une stratégie d’accès au niveau du conteneur, vous pouvez hello autorisations tooadjust de capacité sans avoir tooissue nouvelle URL pour les ressources hello protégées avec des signatures d’accès partagé.
* Les files d’attente Azure pour les files d’attente de ressources d’applications Azure sont toodrive couramment utilisé pour le compte de locataires de traitement, mais peut-être également être utilisés toodistribute travail requis pour configuration et la gestion.
* Un service partagé de files d’attente du Bus de service pour les ressources de l’Application qui tooa de travail push, vous pouvez utiliser une file d’attente unique où chaque locataire-émetteur dispose uniquement autorisations (dérivées des revendications publiées par ACS) toopush toothat file d’attente, tout en les récepteurs hello uniquement à partir du service de hello avoir toopull d’autorisation à partir des données de hello hello file d’attente en provenance de plusieurs clients.

**Services de connexion et de sécurité**

* Azure Service Bus, une infrastructure de messagerie qui se situe entre les applications qui permet de les messages de tooexchange d’une manière faiblement couplée pour améliorer l’échelle et résilience.

**Services de mise en réseau**

Azure offre plusieurs services de mise en réseau prenant en charge l'authentification et améliorant la capacité de gestion de vos applications hébergées. Ces services hello suivants :

* Azure Virtual Network vous permet d'approvisionner et de gérer des réseaux privés virtuels (VPN) dans Azure, ainsi que de lier ceux-ci de façon sécurisée avec l'infrastructure informatique locale.
* Gestionnaire de trafic de réseau virtuel vous permet d’équilibrer tooload le trafic entrant sur Azure hébergé plusieurs services qu’ils s’exécutent dans hello même centre de données ou dans différents centres de données monde hello.
* Azure Active Directory (Azure AD) est un service moderne, basé sur le protocole REST, qui offre des capacités de contrôle d'accès et de gestion des identités pour vos applications dans le cloud. À l’aide d’Azure AD pour les ressources d’Application Azure AD tooprovides un moyen facile d’authentifier et autoriser les utilisateurs toogain accès tooyour applications et services web tout en autorisant hello de toobe d’authentification et d’autorisation prises en charge de votre code.
* Azure Service Bus offre des capacités de messagerie et de flux de données sécurisées pour les applications distribuées et hybrides, telles que les communications entre les applications hébergées sur Azure et les applications et services locaux, sans nécessiter d'infrastructures de sécurité et de pare-feu complexes. À l’aide de relais Service Bus pour toohello des ressources de l’Application de services qui sont exposées comme points de terminaison peuvent appartenir toohello locataire (par exemple, hébergé en dehors du système hello, tels que local), ou ils peuvent être des services fournis spécialement pour hello client ( Étant donné que les données sensibles, spécifique au locataire y transitent).

**Approvisionnement de ressources**

Azure fournit des nouveaux clients de configuration de plusieurs façons pour une application hello. Pour les applications multi-locataires avec un grand nombre de clients, il est généralement nécessaire tooautomate ce processus par activation de l’approvisionnement de libre-service.

* Rôles de travail vous tooprovision et configurer des ressources par locataire (par exemple, lorsqu’un nouveau client s’inscrit ou annule), collecter des mesures de contrôle utiliser et gérer la mise à l’échelle suivant une planification de certaine ou de dépassement de toohello de réponse des seuils de clé indicateurs de performance. Ce même rôle peut également être utilisé toopush solution de toohello mises à jour et mises à niveau.
* Objets BLOB Windows Azure peut être utilisé tooprovision calcul ou des ressources de stockage préinitialisées pour les nouveaux clients tout en fournissant le calcul hello tooprotect conteneur accès au niveau des stratégies de Packages de service, les images de disque dur virtuel et d’autres ressources.
* Options pour l'approvisionnement de ressources de la base de données SQL pour un locataire :
  
  * Langage DDL dans les scripts ou incorporé en tant que ressources au sein d'assemblys
  * Packages DAC SQL Server 2008 R2 déployés par programme
  * Copie à partir d'une base de données de référence principale
  * À l’aide de la base de données importation et exportation tooprovision nouvelles bases de données à partir d’un fichier.

<!--links-->

[Hosting a Multi-Tenant Application on Azure]: http://msdn.microsoft.com/library/hh534480.aspx
[Designing Multitenant Applications on Azure]: http://msdn.microsoft.com/library/windowsazure/hh689716
