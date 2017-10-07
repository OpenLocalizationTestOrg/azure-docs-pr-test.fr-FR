---
title: "Notes de mise à jour d’aaaAzure SDK pour .NET 2.7 et .NET 2.7.1"
description: "Notes de publication du Kit de développement logiciel (SDK) Azure pour .NET 2.7 et .NET 2.7.1"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: 877d070a-9bd5-49b3-8fac-6bb5f65c3554
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 8ec72b0f18702e6d811f0cbe4790685be7881d96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-27-and-net-271-release-notes"></a>Notes de publication du Kit de développement logiciel (SDK) Azure pour .NET 2.7 et .NET 2.7.1
## <a name="overview"></a>Vue d'ensemble
Ce document contient les notes de publication hello pour hello Azure SDK pour .NET 2.7 version. 

document de Hello contient également les notes de publication hello pour hello Azure SDK pour .NET 2.7.1 version.

Le SDK Azure 2.7 est uniquement pris en charge dans Visual Studio 2015 et Visual Studio 2013. [Azure SDK 2.6](https://azure.microsoft.com/downloads/) hello pris en charge dernier Kit de développement logiciel pour Visual Studio 2012.

Pour plus d’informations sur cette version, consultez le [billet d’annonce du Kit de développement logiciel (SDK) Azure 2.7](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) et le [billet d’annonce du Kit de développement logiciel (SDK) Azure 2.7.1](http://go.microsoft.com/fwlink/?LinkId=623850).

## <a name="azure-sdk-for-net-27"></a>Kit de développement logiciel (SDK) Azure pour .NET 2.7
### <a name="sign-in-improvements-for-visual-studio-2015"></a>Améliorations en matière de connexion pour Visual Studio 2015
2.7 de kit de développement logiciel Azure pour Visual Studio 2015 prend en charge les nouvelles fonctionnalités de gestion d’identité hello dans Visual Studio 2015.  Cela inclut la prise en charge des comptes qui accèdent à Azure par le biais du contrôle d’accès en fonction du rôle (RBAC), de fournisseurs de solutions Cloud, de DreamSpark, ainsi que d’autres types de compte et d’abonnement.

Hello connectez-vous améliorations apportées à inclus avec Azure SDK 2.7 sont uniquement disponibles dans Visual Studio 2015. La prise en charge de Visual Studio 2013 est comprise dans le Kit de développement logiciel (SDK) Azure 2.7.1.

### <a name="mobile-sdk"></a>Kit de développement logiciel (SDK) Mobile
Mise à jour **Mobile Apps** tooreflect modèles les plus récents [package NuGet](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) et le processus d’installation.

### <a name="service-bus"></a>Service Bus
Résolutions de bogue et améliorations générales. Pour plus de détails sur les fonctionnalités et les mises à jour, reportez-vous à toohello notes de publication de hello dernières [Service Bus NuGet](http://www.nuget.org/packages/WindowsAzure.ServiceBus/).

### <a name="hdinsight-tools"></a>Outils HDInsight
Dans cette version hello mises à jour suivantes ont été apportées. Ces mises à jour sont disponibles en version préliminaire. Pour plus d’informations, voir [ce blog](http://go.microsoft.com/fwlink/?LinkId=619108).

* Graphiques Hive pour les travaux Hive sur Tez
* Prise en charge complète de la fonctionnalité IntelliSense pour les instructions DML Hive
* Prise en charge des modèles Pig
* Modèles Storm pour les services Azure

#### <a name="breaking-changes"></a>Dernières modifications
* Ancien **Storm** projet doit être mis à niveau lors de l’utilisation de cette version des outils de hello. Pour plus d’informations, consultez [ce blog](http://go.microsoft.com/fwlink/?LinkId=619108).
* Visual Studio Web Express n’est plus pris en charge. Pour plus d’informations, voir [ce blog](http://go.microsoft.com/fwlink/?LinkId=619108).

### <a name="azure-app-service-tools"></a>Outils Azure App Service
Dans cette version hello mises à jour suivantes ont été apportées à tooWeb les Extensions d’outils. Pour plus d’informations, consultez [ce](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/) blog. 

* Nouvelle prise en charge des comptes DreamSpark
* Complète modifier tooAzure outils toosupport hello nouvelles API de gestion de ressources Azure
* Prise en charge pour le Service d’applications Azure ajouté trop[Cloud Explorer](#cloud_explorer)

#### <a name="known-issues"></a>Problèmes connus
Nœuds d’emplacement Web application déploiement n’apparaissent pas sous le nœud des emplacements hello dans l’Explorateur de serveurs et nœuds enfants de l’application Web déploiement emplacement ne sont pas chargés dans Cloud Explorer. Ce problème a été résolu et préparé pour la prochaine version de kit de développement logiciel hello. 

### <a name="cloud_explorer"></a>Cloud Explorer pour Visual Studio 2015
Azure SDK 2.7 inclut Cloud Explorer pour Visual Studio 2015, qui vous permet de tooview vos ressources Azure, examiner leurs propriétés et effectuer des actions de la clé de développeur à partir de Visual Studio. 

Explorateur de cloud prend en charge suivantes d’hello :

* Vues Groupe de ressources et Type de ressource de vos ressources Azure 
* Recherche de ressources par nom (disponible dans la vue Type de ressource)
* Prise en charge des abonnements et des ressources auxquels s’applique le contrôle d’accès en fonction du rôle (RBAC) 
* Panneau de Action intégrée qui affiche les ressources de tooselected spécifique destinés aux développeurs des actions. Par exemple : attacher le débogueur distant pour les ordinateurs virtuels créés à l’aide de hello pile Resource Manager, afficher les données de diagnostic pour etc. de Machines virtuelles.
* Panneau Propriétés intégrées affichant les propriétés pour développeurs généralement nécessaires lors des phases de développement ou de test 
* Le changement rapide d’hello compte toouse lors de l’énumération des ressources (utilisez la commande paramètres sur la barre d’outils) 
* Le filtrage des abonnements toouse lors de l’énumération des ressources (utilisez la commande paramètres sur la barre d’outils) 
* Des liens profonds toohello portail Azure pour la gestion des ressources et des groupes de ressources 

### <a name="azure-resource-manager-tools"></a>Outils du gestionnaire de ressources Azure
Outils Hello Azure Resource Manager ont été mis à jour toowork avec contrôle d’accès en fonction rôle (RBAC) et de nouveaux types d’abonnement.  Inclus avec ces modifications est hello capacité toouse nouveaux comptes de stockage, en outre tooclassic stockage, artefacts toostore pendant le déploiement.  

Si vous utilisez un projet de groupe de ressources Azure à partir d’une version précédente du Kit de développement logiciel de hello avec hello SDK 2.7, un nouveau script de déploiement est toodeploy nécessaire à l’aide d’un compte de stockage au lieu de stockage classiques.  Vous êtes invité avant que les modifications sont apportées de nouveau script tooyour projet tooadd hello.  ancien script de Hello sera renommé et vous devrez toomanually apporter de modifications toohello nouveau script.

### <a name="storage-explorer-tools"></a>Outils de l’Explorateur de stockage
* Prise en charge de l’affichage des types d’objet blob « Append Blob ». Plus d’informations dans [ce billet de blog](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/04/13/introducing-azure-storage-append-blob.aspx). 
* Prise en charge de l’affichage des comptes de stockage Premium par le biais de l’Explorateur de serveurs. L’Explorateur de serveurs affiche uniquement les objets BLOB de pages pour les comptes de stockage premium lorsqu’ils sont de type hello pris en charge uniquement pour les comptes de stockage premium.

### <a name="azure-data-factory-tools-for-visual-studio"></a>Outils d’Azure Data Factory pour Visual Studio
Introduction des **outils d’Azure Data Factory** pour Visual Studio. Voici les fonctionnalités hello activée. Pour plus d’informations, consultez [ce blog](http://go.microsoft.com/fwlink/?LinkId=617530) .

* **Basées sur des modèles de création**: sélectionnez casse utilisation des modèles en fonction, les modèles de déplacement des données ou le traitement des données modèles toodeploy une solution d’intégration des données de bout en bout et démarrer rapidement sur la fabrique de données. 
* **Intégration à l’Explorateur de solutions pour la création et le déploiement d’entités Data Factory** : créez et déployez des pipelines et des entités associées sous la forme de projets Visual Studio. 
* **Intégration à la vue de diagramme pour une interaction visual pendant la création de**: créer visuellement des pipelines et les jeux de données à l’aide de hello vue de diagramme. 
* **Intégration avec l’Explorateur de serveurs pour la navigation et l’interaction avec les entités déjà déployées**: optimisez hello l’Explorateur de serveurs toobrowse est déjà déployé fabriques de données et les entités correspondantes. Importez une fabrique de données déployée ou n’importe quelle entité (pipeline, service lié, jeux de données) dans votre projet. 
* **Modification du code JSON avec validation de schéma et fonctionnalité IntelliSense enrichie**: configurez et modifiez efficacement les documents JSON des entités Data Factory grâce à la puissante fonctionnalité IntelliSense et à la validation de schéma. 
* **Publication de l’environnement multi**: publier l’environnement de production, de test ou de pipelines créés toodev en créant des fichiers de configuration distincts pour chaque environnement.
* **Prise en charge du traitement de données reposant sur Pig, Hive et .NET**: prenez en charge les scripts Pig et Hive dans vos projets Data Factory. Prenez également en charge le référencement de projets C# pour la gestion de .Net Activity.

## <a name="azure-sdk-for-net-271"></a>Kit de développement logiciel (SDK) Azure pour .NET 2.7.1
Hello suivant la section contient des mises à jour qui ont été introduits avec hello Azure SDK pour .NET 2.7.1 version.

### <a name="hdinsight-tools"></a>Outils HDInsight
Pour plus d'explications sur les mises à jour des outils HDInsight, consultez [ce blog](http://go.microsoft.com/fwlink/?LinkId=623831).

* Affichage d’opérateur de tâche de Hive (nouvelle fonctionnalité)
  
    toohelp vous comprenez votre requête Hive mieux, la fonction de la vue d’opérateur Hive hello a été ajouté. toosee tous les opérateurs hello à l’intérieur d’un sommet, double-cliquez sur les sommets hello hello du graphique des travaux. tooview plus d’informations sur un opérateur spécifique, placez le curseur sur cet opérateur.
* Marqueur d'erreur Hive (une nouvelle fonctionnalité)
  
    tooenable que vous tooview hello erreurs de grammaire instantanément, hello fonctionnalité de la ruche d’erroné a été ajouté. En outre, les messages d’erreur ont été améliorées et vous pouvez maintenant voir les erreurs de grammaire détaillées instantanément (jusqu'à ce que cette version, vous avez toosubmit un cluster de toohello script Hive et attente pendant un certain temps avant d’obtenir plus d’informations sur votre message d’erreur).  
* Graphique de topologie Storm (nouvelle fonctionnalité)
  
    La visualisation est très importante lorsque vous souhaitez toosee si votre topologie fonctionne comme prévu. Dans cette version, nous avons ajouté l’affichage des graphes Storm. Vous pouvez visualiser les métriques importantes hello pour votre topologie (par exemple, une couleur indique météo une certaine éclair est « occupée » ou non). Vous pouvez également double-cliquer sur hello éclair/bec tooview plus de détails.
* Prise en charge des clusters HDInsight qui ont été créés dans hello Azure Portal (une résolution de bogue)
  
    Vous pouvez maintenant utiliser Visual Studio tooview et soumettre tooall travaux votre HDInsight clusters quel que soit l’où le cluster de hello ont été créés.
* Plus de prise en charge IntelliSense et un chargement plus rapide des métadonnées Hive (amélioration)
  
    Nous avons amélioré hello IntelliSense en ajoutant plus de suggestions convivial. Par exemple, les alias de table peuvent maintenant être proposés dans IntelliSense pour vous permettre d'écrire plus facilement votre requête. En outre, nous avons amélioré les métadonnées de Hive hello chargement simplement prendra plusieurs secondes toolist toutes les bases de données hello, les tables et les colonnes de votre magasin de métadonnées Hive.

Pour plus d'explications sur les mises à jour des outils HDInsight, consultez [ce blog](http://go.microsoft.com/fwlink/?LinkId=623831).

### <a name="improvements-in-visual-studio-2013"></a>Améliorations dans Visual Studio 2013
* Azure SDK 2.7.1 permet à Visual Studio 2013 tooaccess comptes Azure et des abonnements via Dreamspark Role Based Access Control et les fournisseurs de solutions de Cloud.
* Avec Azure SDK 2.7.1, hello Cloud Explorer fenêtre outil est désormais également disponible dans Visual Studio 2013.

### <a name="known-issues"></a>Problèmes connus
Installation Bonjour Azure SDK 2.6 ou 2.7.1 pour Visual Studio Community 2013 sur un non - anglaise du système d’exploitation affiche un avertissement qui hello anglais et les ressources non anglaises de Visual Studio peuvent ne pas correspondre. Cet avertissement peut être ignoré en toute sécurité. Il se produit uniquement si l’ordinateur de hello ne contenait pas d’une installation antérieure de Visual Studio Community 2013 et que vous installez hello SDK sur un non - anglaise du système d’exploitation. Avertissement de Hello est affiché après que le module linguistique hello applique hello RTM ressources tooVisual Studio, mais avant d’appliquer les mises à jour 4. Ignorez l’avertissement de hello permettra hello language pack toocontinue et la version mise à jour 4 de hello application complète de linguistique hello contenu.

Les projets LightSwitch ne sont pas compatibles avec cette version. Ce problème sera résolu par hello version du Kit de développement logiciel suivant.

## <a name="also-see"></a>Voir aussi
[Billet d’annonce du Kit de développement logiciel (SDK) Azure 2.7.1](http://go.microsoft.com/fwlink/?LinkId=623850)

[Billet d’annonce du Kit de développement logiciel (SDK) Azure 2.7](https://azure.microsoft.com/blog/2015/07/20/announcing-the-azure-sdk-2-7-for-net/)

[Informations pour hello Azure SDK pour .NET et les API et la prise en charge](https://msdn.microsoft.com/library/azure/dn479282.aspx/)

