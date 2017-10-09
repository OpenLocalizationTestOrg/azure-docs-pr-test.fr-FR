---
title: aaaAzure SDK pour .NET 2.6 Notes de publication
description: "Notes de publication du Kit de développement logiciel (SDK) Azure pour .NET 2.6"
services: app-service/web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: b45853d5-a2b8-4962-a22d-579cb36ae14c
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: ac613cf20da4f731fab6f35ccbf6dbeaf18c0ec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-26-release-notes"></a>Notes de publication du Kit de développement logiciel (SDK) Azure pour .NET 2.6
Ce document contient les notes de publication hello pour hello Azure SDK pour .NET 2.6 version. 

Avec Azure SDK 2.6 vous pouvez développer des applications de service cloud (PaaS) ciblant .NET 4.5.2 ou .NET 4.6 autant que vous installez manuellement .NET Framework cible de hello sur hello rôle du Service Cloud. Consultez [Installer .NET sur un rôle de service cloud](http://go.microsoft.com/fwlink/?LinkID=309796).

## <a name="service-bus-updates"></a>Mises à jour Service Bus
* Hubs d'événements : 
  
  * Permettent désormais un contrôle d'accès ciblé lors de l'envoi d'événements avec l'exposition d'un autre point de terminaison de serveur de publication pour les hubs d'événements.
  * Stabilité et l’amélioration a ajouté une fonctionnalité de concentrateurs tooEvent.
  * Ajout de la prise en charge du protocole Amqp sur WebSocket pour la messagerie et les hubs d'événements.

## <a name="hdinsight-tools-for-visual-studio-updates"></a>Mises à jour des outils HDInsight pour Visual Studio
* **Amélioration d'IntelliSense**: suggestion de métadonnées distantes
  
    Les outils HDInsight pour Visual Studio prennent en charge l'obtention de métadonnées distantes pendant la modification d'un script Hive. Par exemple, vous pouvez taper **sélectionner * FROM** et tous les noms de table hello seront affichés. En outre, les noms de colonne hello seront affichera après avoir spécifié une table.
* **Prise en charge de l'émulateur HDInsight**
  
    Maintenant les outils HDInsight pour la prise en charge de Visual Studio connexion tooHDInsight émulateur, donc vous pouvez développer vos scripts Hive localement sans introduire des coûts, puis exécutez ces scripts sur vos clusters HDInsight. 
  
    Pour plus d’informations, consultez trop[ce manuel](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).
* **Prise en charge des clusters Hadoop génériques par les outils HDInsight pour Visual Studio** (version préliminaire)
  
    Maintenant outils HDInsight pour Visual Studio prennent en charge les clusters Hadoop génériques, vous pouvez utiliser les outils HDInsight à la suite Visual Studio toodo hello :
  
  * se connecter tooyour cluster, 
  * Écriture d'une requête Hive avec une prise en charge améliorée d'IntelliSense et de la saisie semi-automatique 
  * afficher tous les travaux de hello dans votre cluster avec une interface utilisateur intuitive. 
    
    Pour plus d’informations, consultez trop[ce manuel](http://go.microsoft.com/fwlink/?LinkID=529540&clcid=0x409).

## <a name="in-role-cache-updates"></a>Mises à jour d'In-Role Cache
* **In-Role Cache** a été mis à jour toouse **SDK Microsoft Azure Storage** version 4.3. Jusqu'à maintenant, hello **In-Role Cache** a été à l’aide de stockage de Azure SDK version 1.7.
  
    Les clients à l’aide d’Azure SDK 2.5 ou ci-dessous doit mettre à jour tooAzure 2.6 du Kit de développement logiciel et déplacer toohello une nouvelle version du SDK de stockage Azure. 
  
    À cette version de stockage Azure temps 2011-08-18 est planifiée toobe supprimé le 1er août 2016. Les migrations de In-Role Cache à partir d’Azure SDK 2.5 ou en dessous too2.6 doivent être terminées en ce moment. Pour plus d’informations sur la retraite hello d’Azure Storage version 2011-08-18, consultez [mise à jour Microsoft Azure Storage Service Version suppression : Extension too2016](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/10/19/microsoft-azure-storage-service-version-removal-update-extension-to-2016.aspx).

> [!IMPORTANT]
> Nous mettons annonce hello avant le 30 novembre 2016, retrait pour un Service de Cache géré Azure et d’Azure In-Role Cache. Nous vous recommandons de migrer tooAzure Cache Redis en préparation de cette suppression. Pour plus d’informations sur les dates et obtenir des conseils de migration, consultez [Quelle offre de cache Azure me convient ?](../redis-cache/cache-faq.md#which-azure-cache-offering-is-right-for-me)
> 
> 

## <a name="azure-app-service-tools"></a>Outils Azure App Service
Hello éléments suivants ont été mis à jour dans la version de hello Azure SDK 2.6.

* Publication Azure améliorée tooinclude Azure API Apps comme une cible de déploiement.
* Applications d’API de configuration des fonctionnalités aux utilisateurs de tooenable avec la création de l’application API et des fonctionnalités de configuration.
* Serveur Explorer modifié tooreflect nouveau nœud App Service, avec les applications Web, mobiles et API regroupé par groupe de ressources.
* Ajouter des mouvements de Client Azure API App ajouté toomost c# les projets qui active la génération automatique de Swagger API applications en cours d’exécution dans un abonnement Azure d’un utilisateur.
* Les outils API Apps et les nœuds App Service de l'Explorateur de serveurs sont uniquement disponibles dans Visual Studio 2013. 

## <a name="azure-resource-manager-tools-updates"></a>Mises à jour des outils du gestionnaire des ressources Azure
outils du Gestionnaire de ressources Azure Hello ont été tooinclude mis à jour des modèles pour les ordinateurs virtuels, de mise en réseau et de stockage. expérience d’édition Hello JSON a été mis à jour tooinclude une nouvelle vue de plan pour les modèles et les modèles d’hello hello capacité tooedit à l’aide d’extraits de code JSON. Les modèles déployés à partir de Visual Studio utilisent un script PowerShell fourni avec le projet de hello, donc toutes les modifications apportées toohello script seront utilisées par Visual Studio.

## <a name="diagnostics-improvements-for-cloud-services"></a>Amélioration des diagnostics pour Cloud Services
Azure SDK 2.6 ramène la prise en charge pour collecter les journaux de diagnostics dans l’émulateur de calcul Azure hello et les transférer toodevelopment stockage. Les diagnostics se connecte (y compris la trace du suivi pour les journaux Windows (ETW), les compteurs de performance, infrastructure de journaux des événements windows et les journaux d’événements, les journaux de l’application) généré lorsque l’application hello s’exécute dans l’émulateur de hello peut être transférée toodevelopment tooverify de stockage qui fonctionne de la journalisation des diagnostics sur votre ordinateur local. 

Hello compte de stockage de Diagnostics peut désormais être spécifié dans fichier de configuration (.cscfg) de service hello rend plus faciles comptes de stockage toouse diagnostics différents pour différents environnements. Il existe des différences notables entre la chaîne de connexion hello travaillé dans Azure SDK 2.4 et 2.6 du Kit de développement logiciel Azure. Pour plus d’informations sur la chaîne de connexion de stockage de Diagnostics toouse hello et son impact sur vos projets voir [configuration des Diagnostics pour Azure Cloud Services](http://go.microsoft.com/fwlink/?LinkID=532784).

## <a name="breaking-changes"></a>Dernières modifications
### <a name="azure-resource-manager-tools"></a>Outils du gestionnaire de ressources Azure
* Hello **projets de déploiement Cloud** disponibles dans Azure SDK 2.5 a été renommé trop de hello du type de projet**groupe de ressources Azure**.
* **Projets de déploiement de cloud computing** type des projets créés dans hello Azure SDK 2.5 peut être utilisé dans 2.6, mais le déploiement du modèle hello à partir de Visual Studio ne fonctionnera pas. Toutefois, le déploiement avec script PowerShell de hello continueront de fonctionner comme il le faisait auparavant.  Pour plus d’informations sur la façon de toouse **projets de déploiement Cloud** dans 2.6 lire ce [valider](http://go.microsoft.com/fwlink/?LinkID=534086).

## <a name="known-issues"></a>Problèmes connus
* Collecter les journaux de diagnostics dans l’émulateur de hello nécessite un système d’exploitation de 64 bits. Les journaux de diagnostic ne seront pas collectés sur les systèmes d'exploitation 32 bits. Cela n'affecte pas les autres fonctionnalités de l'émulateur. 
* Le SDK Azure 2.6 publié le 29/04/2015 présentait deux problèmes : 
  
  * Application universelle n’a pas pu être chargée dans Visual Studio 2015 lors de l’installation sur l’ordinateur de hello Azure SDK 2.6.
  * Débogage d’un projet de Service Cloud échoue dans Visual Studio 2013 et Visual Studio 2015 où Visual Studio cesse de répondre et se bloque lors de l’affichage d’une boîte de dialogue avec un message de type hello « Configuration des diagnostics pour l’émulateur ».
    
    Une mise à jour de tooAzure 2.6 du Kit de développement logiciel a été publié sur 5/18/2015. version de mise à jour de Hello est 2.6.30508.1601 ; Il contient des correctifs pour deux problèmes décrits ci-dessus. Vous pouvez identifier la build hello Hello SDK à partir du Panneau de configuration -> Programmes et fonctionnalités -> Microsoft Azure Tools pour Microsoft Visual Studio 2013 – v 2.6. colonne de Version Hello affichera le numéro de build hello.
    
    Si vous êtes toujours confronté à hello au-dessus de problèmes, hello installer la version plus récente de hello Azure 2.6 SDK pour [Visual Studio 2012](http://go.microsoft.com/fwlink/p/?linkid=323511&clcid=0x409), [VS 2013](http://go.microsoft.com/fwlink/p/?linkid=323510&clcid=0x409) ou [VS 2015](http://go.microsoft.com/fwlink/?linkid=518003&clcid=0x409).

## <a name="see-also"></a>Voir aussi
[Informations pour hello Azure SDK pour .NET et les API et la prise en charge](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

