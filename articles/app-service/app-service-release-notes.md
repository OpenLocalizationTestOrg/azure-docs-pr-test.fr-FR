---
title: "Notes de mise à jour d’aaaAzure SDK pour .NET 2.5.1"
description: "Notes de publication du Kit de développement logiciel (SDK) Azure pour .NET 2.5.1"
services: app-service
documentationcenter: .net,nodejs,java
author: Juliako
manager: erikre
editor: 
ms.assetid: 8d3d815f-bb58-447e-8ff0-f9b9603c7b00
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/10/2016
ms.author: juliako
ms.openlocfilehash: 5ee7688617c966baa409045881c172bbbc55ff63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-251-release-notes"></a>Notes de publication du Kit de développement logiciel (SDK) Azure pour .NET 2.5.1
Ce document contient les notes de publication hello pour hello Azure SDK pour .NET 2.5.1 version. 

## <a name="azure-sdk-for-net-251-release-notes"></a>Notes de publication du Kit de développement logiciel (SDK) Azure pour .NET 2.5.1
Hello Voici les nouvelles fonctionnalités et mises à jour Bonjour Azure SDK pour .NET 2.5.1.

* Nouveaux scénarios liés trop**Extensions des outils Web**. 
  
  * Sites Web Azure a été renommé tooAzure du Service d’applications. Pour plus d’informations, consultez [Azure App Service et services Azure existants](../app-service-web/app-service-changes-existing-services.md).
  * Prise en charge de Azure (aperçu) les applications API a été ajouté afin que les clients peuvent publier des projets ASP.NET en tant qu’applications de l’API et ensuite utiliser hello Ajouter > mouvement du Client Azure API App dans les projets toogenerate code c# basé sur la structure hello Hello déployé l’application API. 
  * nœud de sites Web Hello dans l’Explorateur de serveurs a été déconseillée au lieu de nœud de Service d’applications Azure hello, qui prend en charge pour la ressource de groupe-en fonction de regroupement des applications API Azure, les applications mobiles et les applications Web.
  * Prise en charge de Azure Mobile Apps (version préliminaire) a été ajouté afin que les clients peuvent créer des projets d’applications mobiles, ajouter des applications mobiles contrôleurs, publier des projets de hello et déboguer à distance.
  * Ajouter > mouvement du Client Azure API App prend désormais en charge les fichiers JSON de Swagger locaux, permet aux développeurs des API Web NuGets tiers comme Swashbuckle toogenerate Swagger ou créez-la manuellement. De cette manière, client les développeurs peuvent utiliser tooconsume de fonctionnalités de génération de code hello n’importe quel point de terminaison Swagger dans les projets c#. 
  * Application Web et application API de boîtes de dialogue de publication ont été améliorées toosupport concept de portail Azure hello de ressource de regroupement et sélection/création de groupes de ressources Azure et de Plans de Service d’application sont représentés dans hello nouvelle application Web et application API approvisionnement boîte de dialogue. 
  * Nœuds d’Explorateur de serveurs d’application API Azure fournissent toohello liens qu'approfondie des applications API lier dans hello portail Azure, ainsi que d’autres fonctionnalités telles que les journaux de diffusion en continu et le débogage distant.
    
    Pour les problèmes connus et les limites actuelles dans le Kit de développement logiciel (SDK) Azure pour .NET 2.5.1, consultez la [section](app-service-release-notes.md#known_issues_2_5_1) ci-dessous.
* Nouveaux scénarios liés trop**outils HDInsight** dans Visual Studio sont activés dans cette version. 
  
  * Validation locale des scripts Hive. Cliquez sur bouton de script de validation hello dans hello barre d’outils toosee s’il existe des erreurs dans votre script. 
  * Débogage amélioré des tâches Hive. Vous pouvez maintenant déboguer les tâches Hive en accédant aux journaux Yarn dans Visual Studio. Si votre application présente des problèmes de performances, l'examen des journaux Yarn fournit des informations utiles.
  * (Version préliminaire publique) Prise en charge d'IntelliSense et de la saisie semi-automatique des mots clés pour Hive. toohelp vous créez des scripts Hive, outils HDInsight pour Visual Studio ajouté la saisie semi-automatique (mot clé) et la prise en charge IntelliSense pour la ruche.
  * Prise en charge de Storm. Vous pouvez désormais utiliser les outils HDInsight pour Visual Studio toodevelop Storm topologies/becs verseurs/boulons en c#. Vous pouvez ensuite envoyer hello développé cluster Storm de tooa topologie et consultez le statut de topologie/éclair/bec hello. Vous pouvez utiliser les journaux système et le client connecte tootroubleshoot votre Storm topologies/boulons/becs verseurs. Vous pouvez également utiliser les ressources JAVA existantes dans Storm sur HDInsight.
    
    Pour plus d’informations, consultez la page [Prise en main de HDInsight Hadoop Tools pour Visual Studio](../hdinsight/hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a id="known_issues_2_5_1"></a>Limitations et problèmes connus du Kit de développement logiciel (SDK) Azure pour .NET 2.5.1
* Azure API Apps apparaît sous la forme d'une cible de déploiement pour Mobile Apps. Applications Web doit être seule destination de hello pour les applications mobiles que dans une version ultérieure. 
* Configuration de l’application API Azure peut entraîner la réussite, mais par intermittence échouent tooupdate hello progression dans la fenêtre de l’activité de Service d’application Azure hello. Solution de contournement est état toocheck de l’API Azure nouvelle application hello Bonjour portail Azure. 
* La séquence Fichier > Nouveau projet > Application API > F5 provoque une erreur HTTP, car il n'existe aucun fichier default/index.html. Solution de contournement est toomanually Parcourir toohello/api/valeurs URL. 
* Par intermittence, les icônes de l'Explorateur de serveurs apparaissent aplaties. Le redémarrage de Visual Studio résout ce problème. 
* Si une exception est levée pendant la mise en service de l’application Web ou application API (par exemple, les erreurs de quota dépassé ou nom de la passerelle application API Azure en double), erreurs de hello affichent du texte JSON brut. 
* Problèmes intermittents de création de projet quand Application Insights est vérifié au moment de la création du projet.
* Parfois, code de Client Azure API App hello généré manque des espaces de noms, ils doivent toobe inclus manuellement (ou importées automatiquement via les signaux de Visual Studio) pour le code toocompile. 
* Projets d’application mobile doivent être publiée tooweb applications, mais vous devez sélectionner un site que vous avez créé en tant qu’une application Mobile Bonjour Azure Portal, étant donné que les projets de l’application Mobile nécessitent une base de données. 
* page de démarrage Hello pour les applications mobiles utilise le terme hello « service mobile » au lieu de « applications mobiles » 
* La création du projet de l’application mobile peut prendre jusqu'à toocreate minute de tooa. 
* Au cours de l’application API de configuration, dans certains cas, une erreur est restauré à partir de refléter l’API Azure hello que hello Impossible de définir des autorisations correctement, hello application API a été correctement configurée et qu’il est prêt à être utilisé lors de la. Vous pouvez définir manuellement les autorisations à l’aide de hello portail Azure.
* Application Insights n'est pas pris en charge sur les modèles d'application API et les modèles d'application mobile.
* Les projets d'application API ne peuvent pas être utilisés conjointement avec des projets de service cloud.
* Les modèles de projet d'application API sont disponibles uniquement en C#.
* Consommation de l’application API via le menu contextuel de « Ajouter un Client Azure API App » hello est uniquement pris en charge en c#.

