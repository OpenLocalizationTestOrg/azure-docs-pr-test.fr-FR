---
title: aaaAzure SDK pour .NET 2.8 Notes de publication
description: "Notes de publication du Kit de développement logiciel (SDK) Azure pour .NET 2.8"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: de7207ff-ba4f-4008-9141-8742fcaa3254
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 2722dcdd27bf9ab65b48e91dcdb545536f987dd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a>Kit de développement logiciel (SDK) Azure pour .NET 2.8, 2.8.1 et 2.8.2
## <a name="overview"></a>Vue d'ensemble
Cet article contient hello notes de publication (qui inclut les problèmes connus et les modifications avec rupture) pour hello Azure SDK pour .NET 2.8, 2.8.1 et point 2.8.2 libère. 

Pour obtenir une liste complète des nouvelles fonctionnalités et mises à jour effectuées dans cette version, consultez hello [2.8 du Kit de développement logiciel Azure pour Visual Studio 2013 et Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) annonce. 

## <a name="azure-sdk-for-net-28"></a>Kit de développement logiciel (SDK) Azure pour .NET 2.8
### <a name="download-azure-sdk-for-net-28"></a>Télécharger le Kit de développement logiciel (SDK) Azure pour .NET 2.8
[Kit de développement logiciel (SDK) Azure .NET 2.8 pour Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkId=699285) 

[Kit de développement logiciel (SDK) Azure .NET 2.8 pour Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a>Prise en charge de .NET 4.5.2
#### <a name="known-issues"></a>Problèmes connus
2.8 de kit de développement .NET Azure permet de vous toocreate .NET 4.5.2 Service Cloud. Toutefois 4.5.2 de .NET framework n’est pas installé sur les images de système d’exploitation invité jusqu'à ce que le système d’exploitation invité de janvier 2016 de version de la valeur par défaut hello. Avant cela, .NET Framework 4.5.2 sera disponible via une version de système d’exploitation invité distincte, celle de novembre 2015-02. Consultez hello [versions de système d’exploitation invité Azure et matrice de compatibilité SDK](../cloud-services/cloud-services-guestos-update-matrix.md) tootrack page lors de l’image de hello est libérée.  Une fois l’image de hello novembre 2015-02 est libérée. vous pouvez choisir toouse cette image en mettant à jour votre fichier de fichier (.cscfg) de configuration de Service Cloud. Dans la configuration du service hello fichier défini attribut osVersion de hello de chaîne de toohello hello ServiceConfiguration élément » WA-GUEST-OS-4.26_201511-02 ». Si vous choisissez tooopt dans toouse cette image vous n’avez plus obtenez toohello de mises à jour automatiques du système d’exploitation invité. tooget hello mises à jour automatiques hello osVersion doit être définie trop « * » et .NET 4.5.2 n’est disponible par le biais des mises à jour automatiques de janvier 2016.

### <a name="azure-data-factory"></a>Azure Data Factory
#### <a name="known-issues"></a>Problèmes connus
Pendant un **modèle de fabrique de données** projet Création impliquant exemples de données, script azure PowerShell risquent d’échouer si azure power shell version est installée sur l’ordinateur de hello est après 0.9.8.

Dans l’ordre toosuccessfully créer ce type de projet, vous devez installer [version d’interpréteur de commandes azure power 0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi).

### <a name="azure-resource-manager-tools"></a>Outils du gestionnaire de ressources Azure
#### <a name="breaking-changes"></a>Dernières modifications
Hello fourni par le projet de groupe de ressources Azure hello de script PowerShell a été mis à jour dans cette toowork version hello nouveau Azure applets de commande PowerShell version 1.0.  Ce nouveau script fonctionnera pas à partir d’avec Visual Studio lorsque vous utilisez une version de too2.8 préalable du Kit de développement logiciel hello.  

Scripts des projets créés dans les versions antérieures du Kit de développement logiciel de hello ne seront exécute pas à partir de Visual Studio lorsqu’à l’aide de hello SDK 2.8.  Tous les scripts continue toowork en dehors de Visual Studio avec la version appropriée de hello Hello applets de commande PowerShell de Azure.  

Hello 2,8 SDK nécessite la version 1.0 de hello applets de commande PowerShell de Azure.  Toutes les autres versions du Kit de développement logiciel de hello nécessitent la version 0.9.8 de hello applets de commande PowerShell de Azure.  Pour plus d’informations, consultez [ce blog](http://go.microsoft.com/fwlink/?LinkID=623011) .

### <a name="web-tools-extensions"></a>Web Tools Extensions
#### <a name="known-issues"></a>Problèmes connus
Hello suivant problèmes connus est abordé dans hello suivant la mise en production.

* Les mouvements de l’Explorateur de serveurs et du cloud en lien avec App Service pour les environnements autres que ceux de production (comme les clients Azure China ou Azure Stack) ne fonctionnent pas. Pour publier des clients dans ces domaines concernés, téléchargement hello profil hello portail Azure activer la possibilité de publication. Une version ultérieure permettra de réparer les mouvements tels que « Attacher le débogueur » et « Afficher les journaux de diffusion en continu » pour les clients Azure China et Stack. 
* Les clients peuvent voir des erreurs au cours du Service d’applications de création de hello application Insights toowhich qu’ils déploient de l’instance est dans une région autre que les États-Unis. Dans ces scénarios, la création d’un Service d’application dans le portail de hello et le téléchargement de hello profil de publication permet des scénarios de publication. 

### <a name="azure-hdinsight-tools"></a>Outils Azure HDInsight
#### <a name="new-updates"></a>Nouvelles mises à jour
* Vous pouvez exécuter votre requête Hive cluster hello via HiveServer2 avec pratiquement aucune charge mémoire et voir le travail de hello se connecte en temps réel.
* À l’aide de hello nouvelle ruche tâche d’exécution vue votre travail plus profond, vous pouvez explorer plus d’informations et identifier les problèmes potentiels.

Pour plus d’informations, consultez la page relative au [Kit de développement logiciel (SDK) Azure 2.8 pour Visual Studio 2013 et Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/). 

## <a name="azure-sdk-for-net-281"></a>Kit de développement logiciel (SDK) Azure pour .NET 2.8.1
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a>Problèmes connus de Visual Studio 2013 et Visual Studio 2015
1. La tâche Web déclenchée publie tooslots va afficher et erreur et ne sera pas définir un calendrier, mais il transmet tooAzure de la tâche Web hello. Les clients ayant besoin d’un travail planifié peuvent ensuite utiliser tooset du portail Azure hello planification de hello pour hello la tâche Web. 
2. Les utilisateurs Python peuvent rencontrer des problèmes de débogueur. Équipe du service développe un correctif pour ce mais s’ils sont affectés, veuillez laisser Microsoft savoir sur les forums hello ou sur le blog de l’annonce hello ou section de commentaires de notes de version. 
3. Dans certaines régions (par exemple, l’Inde du Sud), les clients sont confrontés à des erreurs d’approvisionnement d’App Service. Cela est cohérent avec le portail de hello, et les clients qui rencontrent ce problème peuvent utiliser hello toorequest portail Azure accès toopublish toothese régions à zones géographiques. Une fois qu’ils demandent des régions de toothese d’accès à l’aide de hello approvisionnement portail Azure doit fonctionner. 

## <a name="azure-sdk-for-net-282"></a>Kit de développement logiciel (SDK) Azure pour .NET 2.8.2
Hello l’installation des outils de hello point 2.8.2, les clients peuvent être confrontés hello suivant le problème.         

* Si vous utilisez Windows 10 et que vous n’avez pas installé Internet Explorer, vous pouvez obtenir l’erreur « Internet Explorer est introuvable ».
  problème de hello tooresolve, installez Internet Explorer à l’aide de hello ajouter/supprimer des composants Windows de boîte de dialogue.

Si vous constatez ce problème, utilisez hello envoyer un sourire fonctionnalité tooreport il.

Pour plus d’informations, consultez [ce billet](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) .

## <a name="other-updates"></a>Autres mises à jour
Pour les autres mises à jour, consultez [Billet d’annonce du Kit de développement logiciel (SDK) Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="also-see"></a>Voir aussi
[Billet d’annonce du Kit de développement logiciel (SDK) Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[Informations pour hello Azure SDK pour .NET et les API et la prise en charge](https://msdn.microsoft.com/library/azure/dn479282.aspx)

