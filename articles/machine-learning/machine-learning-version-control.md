---
title: aaaALM dans Azure Machine Learning | Documents Microsoft
description: "Appliquer les meilleures pratiques d’Application Lifecycle Management dans Azure Machine Learning Studio"
keywords: "ALM, AML, Azure ML, Gestion du cycle de vie des applications, Contrôle de version"
services: machine-learning
documentationcenter: 
author: hning86
manager: jhubbard
editor: cgronlun
ms.assetid: 1be6577d-f2c7-425b-b6b9-d5038e52b395
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: haining
ms.openlocfilehash: 99470ff72fea7ab59d9d44f3fded7b9dd49a38c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-lifecycle-management-in-azure-machine-learning-studio"></a>Application Lifecycle Management dans Azure Machine Learning Studio
Azure Machine Learning Studio est un outil pour développer des expériences d’apprentissage automatique qui sont mis dans la plateforme de cloud computing Azure hello. C’est comme hello IDE de Visual Studio et le service de cloud évolutives fusionnées dans une seule plateforme. Vous pouvez incorporer des pratiques d’Application Lifecycle Management (ALM) standard, à partir du contrôle de version différents de déploiement et de l’exécution de tooautomated de ressources dans Azure Machine Learning Studio. Cet article décrit certains des approches et des options de hello.

## <a name="versioning-experiment"></a>Contrôle de version d’expérience
Il existe deux méthodes recommandées tooversion vos expériences. Vous pouvez s’appuient sur l’historique d’exécution intégré, ou exporter expérience hello dans format JavaScript Objet Notation (JSON) et gérer de façon externe. Chaque approche présente des avantages et des inconvénients.

### <a name="experiment-snapshots-using-run-history"></a>Instantanés d’expérience à l’aide de l’historique d’exécution
Dans le modèle d’exécution hello Hello expérience d’apprentissage d’Azure Machine Learning Studio, chaque fois que vous cliquez sur hello **exécuter** bouton dans l’éditeur de test de hello, un instantané immuable d’expérience de hello est envoyé toohello planificateur. Vous pouvez afficher cette liste d’instantanés en cliquant sur hello **historique d’exécution** bouton de barre de commandes hello en hello expérience éditeur.

![Bouton Historique d’exécution](media/machine-learning-version-control/runhistory.png)

Vous pouvez ensuite instantané hello ouvert en mode verrouillé en cliquant sur nom hello d’expérimentation hello au niveau de l’expérience de hello hello temps a été soumis toorun et hello instantané a été pris. Notez que seuls hello premier élément dans la liste hello, qui représente l’expérience actuelle de hello, est dans un état modifiable. Notez également que chaque instantané peut présenter plusieurs états différents, notamment Terminé (Exécution partielle), Échec, Échec (exécution partielle) ou Brouillon.

![Liste Historique d’exécution](media/machine-learning-version-control/runhistorylist.png)

Après qu’il a ouverte, vous pouvez enregistrer hello instantané expérience en tant qu’une nouvelle expérience et puis le modifier. Si votre instantané de l’expérience contient des ressources telles que le modèle formé, de transformation et de jeu de données qui ont des versions mises à jour, instantané d’hello conserve version d’origine de hello références toohello hello instantané a été pris. Si vous enregistrez hello verrouillé instantané comme une nouvelle expérience, Azure Machine Learning Studio détecte l’existence de hello d’une version plus récente de ces ressources et les met à jour automatiquement dans l’expérience de nouveau hello.

Si vous supprimez expérience de hello, tous les instantanés de cette expérience sont supprimés.

### <a name="exportimport-experiment-in-json-format"></a>Importation/exportation d’expérience au format JSON
instantanés d’historique Hello exécuter conserver une version immuable de hello expérience dans Azure Machine Learning Studio chaque fois qu’il est soumis toorun. Vous pouvez également enregistrer une copie locale de l’expérience de hello et archivez-le dans le système de contrôle de source de favoris tooyour, tel que Team Foundation Server et version ultérieure sur recréer une expérience à partir de ce fichier local. Vous pouvez utiliser hello [Azure Machine Learning PowerShell](http://aka.ms/amlps) applets de commande [ *Export-AmlExperimentGraph* ](https://github.com/hning86/azuremlps#export-amlexperimentgraph) et [  *Importer-AmlExperimentGraph* ](https://github.com/hning86/azuremlps#import-amlexperimentgraph) tooaccomplish qui.

fichier JSON de Hello est une représentation textuelle de hello expérimenter graphique, ce qui peut inclure un tooassets de référence dans l’espace de travail de hello comme un jeu de données ou un modèle formé. Il ne contient pas une version sérialisée d’un élément multimédia de hello. Si vous essayez de document JSON de hello tooimport dans l’espace de travail hello, les ressources hello référencé doivent déjà exister avec hello même asset ID qui sont référencés dans l’expérience de hello. Dans le cas contraire, vous ne serez pas en mesure de tooaccess hello importé expérience.

## <a name="versioning-trained-model"></a>Contrôle de version du modèle formé
Un modèle formé dans Azure Machine Learning est sérialisé dans un format appelé un fichier .iLearner et est stocké dans le compte de stockage d’objets Blob Azure hello associée hello espace de travail. Une façon tooget une copie du fichier de .iLearner hello est hello réapprentissage API. [Cet article](machine-learning-retrain-models-programmatically.md) explique le fonctionne de hello réapprentissage API. Hello principales étapes à suivre :

1. Configurez votre expérience de formation.
2. Ajouter un module Train Model toohello du port sortie web service ou le module hello qui génère le modèle formé hello, telles que Hyperparameter de modèle paramétrer ou Create R Model.
3. Exécutez votre expérience de formation et déployez-la en tant que service web de formation de modèle.
4. Appeler hello point de terminaison BES du service web de formation hello et spécifiez le nom hello .iLearner souhaitée et l’emplacement de compte de stockage Blob où il sera stocké.
5. Récolte hello produit .iLearner fichier après l’appel de hello BES se termine.

Un autre fichier .iLearner de façon tooretrieve hello est via l’applet de commande PowerShell hello [ *AmlExperimentNodeOutput de téléchargement*](https://github.com/hning86/azuremlps#download-amlexperimentnodeoutput). Cela peut être plus facile si vous souhaitez simplement tooget une copie de hello .iLearner fichier sans modèle de hello tooretrain hello besoin par programme.

Après avoir configuré les fichiers de .iLearner hello contenant le modèle formé de hello, vous pouvez ensuite utiliser votre propre stratégie de contrôle de version. stratégie de Hello peut être aussi simple qu’appliquant un pré/suffixe comme une convention d’affectation de noms et de simplement laisser fichier .iLearner de hello dans le stockage Blob ou de copie/importer dans votre système de contrôle de version.

Hello enregistré .iLearner fichier peut ensuite être utilisé pour calculer les scores via les services web déployé.

## <a name="versioning-web-service"></a>Contrôle de version du service web
Vous pouvez déployer deux types de services web à partir d’une expérience Azure Machine Learning. service web classique de Hello est étroitement avec l’expérience de hello ainsi que d’espace de travail hello. nouveau service web de Hello utilise l’infrastructure du Gestionnaire de ressources Azure hello et elle est associée n’est plus l’expérience d’origine de hello ou un espace de travail hello.

### <a name="classic-web-service"></a>Service web classique
tooversion un service web classique, vous pouvez tirer parti de la construction de point de terminaison hello web service. Voici un flux typique :

1. À partir de votre expérience prédictive, vous déployez un nouveau service web classique qui contient un point de terminaison par défaut.
2. Vous créez un nouveau point de terminaison nommé ep2, qui expose la version actuelle de hello du modèle d’apprentissage / l’expérience hello.
3. Vous revenez en arrière et mettez à jour votre expérience prédictive et le modèle formé.
4. Vous redéployez l’expérience prédictive hello, qui met ensuite à jour de point de terminaison par défaut hello. Mais cela ne modifie en rien ep2.
5. Vous créez un point de terminaison supplémentaire nommé ep3, qui expose la nouvelle version de hello d’essais de hello et le modèle formé.
6. Revenir en arrière toostep 3 si nécessaire.

Au fil du temps, vous pouvez avoir plusieurs points de terminaison créés Bonjour même service web. Chaque point de terminaison représente une copie de point-à-temps d’expérimentation hello contenant la version de point-à-temps hello du modèle formé de hello. Vous pouvez ensuite utiliser toodetermine logique externe qui toocall de point de terminaison, ce qui signifie que la sélection d’une version de hello formé de modèle pour calculer les scores hello exécuter.

Vous pouvez également créer plusieurs points de terminaison de service web identiques et puis de correctif logiciel des versions différentes de hello .iLearner fichier toohello point de terminaison tooachieve des effets similaires. [Cet article](machine-learning-create-models-and-endpoints-with-powershell.md) explique en détail comment tooaccomplish qui.

### <a name="new-web-service"></a>Nouveau service web
Si vous créez un nouveau service web basé sur le Gestionnaire de ressources Azure, construction de point de terminaison hello n’est plus disponible. Au lieu de cela, vous pouvez générer des fichiers de définition (WSD) du service web, au format JSON, à partir de votre expérience prédictif à l’aide de hello [Export-AmlWebServiceDefinitionFromExperiment](https://github.com/hning86/azuremlps#export-amlwebservicedefinitionfromexperiment) applet de commande PowerShell, ou à l’aide de hello [ *Export-AzureRmMlWebservice* ](https://msdn.microsoft.com/library/azure/mt767935.aspx) applet de commande PowerShell d’un service déployé web basé sur le Gestionnaire de ressources.

Une fois que vous avez hello exportée contrôlent de version et le fichier WSD, vous pouvez également déployer hello WSD comme un service web dans un plan de service web différents dans une région différente. Assurez-vous simplement que vous fournissez le compte de stockage approprié hello configuration ainsi que hello new web ID de plan de service. toopatch dans les fichiers de .iLearner différents, vous pouvez modifier un fichier WSD de hello et mise à jour la référence d’emplacement hello Hello formé de modèle et déployez-le en tant qu’un nouveau service web.

## <a name="automate-experiment-execution-and-deployment"></a>Automatiser le déploiement et l’exécution de l’expérience
Un aspect important de ALM est l’exécution de toobe tooautomate en mesure de hello et processus de déploiement d’application hello. Dans Azure Machine Learning, procéder à l’aide de hello [module PowerShell](http://aka.ms/amlps). Voici un exemple de bout en bout pour les étapes qui sont des processus d’exécution/déploiement ALM automatisée standard de tooa pertinentes à l’aide de hello [module PowerShell de Azure Machine Learning Studio](http://aka.ms/amlps). Chaque étape est lié tooone ou plusieurs applets de commande PowerShell que vous pouvez utiliser tooaccomplish auquel l’étape.

1. [Téléchargez un jeu de données](https://github.com/hning86/azuremlps#upload-amldataset).
2. Copier une expérience d’apprentissage dans l’espace de travail hello à partir d’un [espace de travail](https://github.com/hning86/azuremlps#copy-amlexperiment) ou à partir de [galerie](https://github.com/hning86/azuremlps#copy-amlexperimentfromgallery), ou [importer](https://github.com/hning86/azuremlps#import-amlexperimentgraph) un [exporté](https://github.com/hning86/azuremlps#export-amlexperimentgraph) tester à partir de disque local.
3. [Mettre à jour le jeu de données hello](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) dans une expérience de formation hello.
4. [Exécutez l’expérience de formation hello](https://github.com/hning86/azuremlps#start-amlexperiment).
5. [Promouvoir le modèle formé de hello](https://github.com/hning86/azuremlps#promote-amltrainedmodel).
6. [Copier une expérience prédictive](https://github.com/hning86/azuremlps#copy-amlexperiment) dans l’espace de travail hello.
7. [Modèle formé de mise à jour hello](https://github.com/hning86/azuremlps#update-amlexperimentuserasset) dans expérience prédictive de hello.
8. [Exécutez expérience prédictive de hello](https://github.com/hning86/azuremlps#start-amlexperiment).
9. [Déployer un service web](https://github.com/hning86/azuremlps#new-amlwebservice) à partir de l’expérience de prédictive hello.
10. Tester un service web de hello [RR](https://github.com/hning86/azuremlps#invoke-amlwebservicerrsendpoint) ou [BES](https://github.com/hning86/azuremlps#invoke-amlwebservicebesendpoint) point de terminaison.

## <a name="next-steps"></a>Étapes suivantes
* Télécharger hello [Azure Machine Learning Studio PowerShell](http://aka.ms/amlps) tooautomate module et démarrer vos tâches ALM.
* Découvrez comment trop[créer et gérer un grand nombre de modèles de ML à l’aide de simplement une expérience unique](machine-learning-create-models-and-endpoints-with-powershell.md) via PowerShell et API de recyclage.
* Découvrez plus d’informations sur le [déploiement de services web Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).
