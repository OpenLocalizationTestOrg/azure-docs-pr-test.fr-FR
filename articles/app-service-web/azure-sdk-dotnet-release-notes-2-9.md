---
title: aaaAzure SDK pour .NET 2.9 Notes de publication
description: "Notes de publication du Kit de développement logiciel (SDK) Azure pour .NET 2.9"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a>Notes de publication du Kit de développement logiciel (SDK) Azure pour .NET 2.9

Cette rubrique comprend des notes de publication relatives aux versions 2.9 et 2.9.6 du Kit SDK Azure pour .NET.

##<a name="azure-sdk-for-net-296-release-summary"></a>Synthèse de publication du Kit SDK Azure pour .NET 2.9.6

Date de lancement : 16/11/2016
 
Aucune toohello de modifications avec rupture Azure SDK 2.9 n’ont été introduites dans cette version. Il n’existe également aucune tooleverage de mise à niveau si nécessaire ce SDK avec les projets de Service Cloud existants.

### <a name="visual-studio-2017-release-candidate"></a>Version finale de Visual Studio 2017

- Dans Visual Studio 2017 RC, cette version de hello Azure SDK pour .NET est intégrée dans hello la charge de travail Azure. Tous les outils hello vous devez toodo le développement Azure feront partie de Visual Studio RC 2017 à l’avenir. Pour Visual Studio 2015 et Visual Studio 2013, hello SDK seront toujours disponible via WebPI. Nous arrêterons d’équiper les versions du Kit SDK Azure pour .NET pour Visual Studio 2013 au moment du lancement de la version finale de Visual Studio 2017. Suivez cette toodownload lien Visual Studio 2017 RC : https://www.visualstudio.com/vs/visual-studio-2017-rc/

### <a name="azure-diagnostics"></a>Azure Diagnostics

- Tooonly de comportement modifié hello stocker une chaîne de connexion partielle avec clé hello remplacé par un jeton de chaîne de connexion de stockage de diagnostics Services de cloud computing. clé de stockage réel Hello est maintenant stockée dans le dossier du profil utilisateur hello pour son accès peut être contrôlé. Visual Studio lit la clé de stockage hello dans le dossier de profil utilisateur pour le débogage local et le processus de publication. 
- Dans la réponse toohello modification est décrite ci-dessus, Visual Studio Online de l’équipe étendu hello modèle de tâche de déploiement de Services de cloud computing Azure utilisateurs peuvent spécifier la clé de stockage hello pour définir l’extension diagnostics lors de la publication tooAzure dans l’intégration continue et le déploiement.
- Nous nous efforçons de chaîne de connexion sécurisée toostore possibles et la création de jetons pour Azure Diagnostics (WAD), toohelp vous résoudre des problèmes de configuration entre multiprotocole.
 
### <a name="windows-server-2016-virtual-machines"></a>Machines virtuelles Windows Server 2016

- Visual Studio prend désormais en charge le déploiement des Services de Cloud tooOS ordinateurs virtuels de famille 5 (Windows Server 2016). Pour les services cloud existants, vous pouvez modifier votre tootarget paramètres hello nouvelle famille de systèmes d’exploitation. Lors de la création de nouveaux services de cloud, si vous choisissez le service de hello toocreate à l’aide de .net 4.6 ou ultérieure, il prend par défaut hello service toouse 5 de famille du système d’exploitation.  Pour plus d’informations, vous pouvez consulter hello [famille de systèmes d’exploitation invité prend en charge la table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).

#### <a name="known-issues"></a>Problèmes connus

- Azure SDK .NET 2.9.6 a introduit une restriction qui bloque le déploiement de projets à l’aide de tooany d’infrastructures (telles que .NET 4.6) non pris en charge .NET famille de système d’exploitation < 5. Une solution de contournement est fournie [ici](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).

 
### <a name="azure-in-role-cache"></a>In-Role Cache Azure 

- La prise en charge d’Azure In-Role Cache prend fin le 30 novembre 2016. Pour plus de détails, cliquez [ici](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).

### <a name="azure-resource-manager-templates-for-azure-stack"></a>Modèles Azure Resource Manager pour Azure Stack

- Nous avons introduit Azure Stack en tant que cible de déploiement pour vos modèles Azure Resource Manager.


## <a name="azure-sdk-for-net-29-summary"></a>Synthèse du Kit SDK Azure pour .NET 2.9

## <a name="overview"></a>Vue d'ensemble
Ce document contient les notes de publication hello pour hello Azure SDK pour .NET 2.9 version. 

Pour plus d’informations sur les mises à jour dans cette version, consultez hello [post d’annonce Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a>Aperçu du Kit de développement logiciel (SDK) 2.9 pour Visual Studio 2015 Update 2 et Visual Studio "15"
Cette mise à jour inclut hello suivant les correctifs de bogues :

* Émettre tooREST connexe API Client génération dans la chaîne hello « Type inconnu » apparaît en tant que nom hello du dossier de génération de code hello et/ou nom hello d’espace de noms hello déposé dans le code de hello généré.
* Émettre WebJobs tooScheduled connexes dans le hello, informations d’authentification a échoué toobe passé le processus d’approvisionnement toohello du planificateur.

Cette mise à jour inclut hello suivant la nouvelle fonctionnalité :

* Prise en charge pour les Services d’application secondaire hello onglet « Services » de hello boîte de dialogue Configuration du Service d’applications. 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a>Outils Azure Data Lake pour Visual Studio 2015 Update 2
Cette mise à jour inclut hello qui suit :

* **Azure Data Lake Tools** pour Visual Studio est maintenant fusionnée à hello Azure SDK pour cette version de .NET. Hello outil est automatiquement installé lorsque vous installez le Kit de développement logiciel Azure. 
  
    outil de Hello est fréquemment mis à jour, accédez [ici](http://aka.ms/datalaketool) tooget hello les mises à jour.
* **L’Explorateur de serveurs** maintenant vous tooview tous les et créer des entités de métadonnées U-SQL. Pour plus d’informations, consultez [ce](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.

## <a name="hdinsight-tools"></a>Outils HDInsight
**Outils HDInsight** pour Visual Studio prennent maintenant en charge HDInsight version 3.3, y compris l'affichage des graphiques Tez et d'autres correctifs de langage.

## <a name="azure-resource-manager"></a>Azure Resource Manager
Cette version ajoute la prise en charge de [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) pour les modèles Resource Manager.

## <a name="see-also"></a>Voir aussi
[Billet d’annonce du Kit de développement logiciel (SDK) Azure 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

