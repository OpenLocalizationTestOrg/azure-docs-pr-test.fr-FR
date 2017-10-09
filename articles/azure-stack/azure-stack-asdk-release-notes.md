---
title: "Notes de mise à jour du Kit de développement Azure pile aaaMicrosoft | Documents Microsoft"
description: 
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: helaw
ms.openlocfilehash: c1644f224933a63e1f0265b6ef4113789900cf12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-development-kit-release-notes"></a>Notes de publication du kit de développement Azure Stack
Ces notes de publication fournissent des informations sur les nouvelles fonctionnalités et les problèmes connus.

## <a name="release-build-201706271"></a>Version 20170627.1
En commençant par hello [20170627.1](azure-stack-updates.md#determine-the-current-version) version, Azure pile preuve de Concept a été renommé tooAzure Kit de développement de pile.  Comme preuve de concept de pile Azure de hello, Kit de développement de pile Azure vise toobe un développement et environnement d’évaluation utilise des fonctionnalités d’Azure pile tooexplore et fournissent une plateforme de développement pour la pile de Azure.

### <a name="whats-new"></a>Nouveautés
- Vous pouvez maintenant utiliser des ressources de pile de Azure toomanage CLI 2.0 à partir d’une ligne de commande sur les systèmes d’exploitation courants.
- Les tailles de machine virtuelle DSV2 assurent la portabilité des modèles entre Azure et Azure Stack.
- Les opérateurs cloud peuvent afficher un aperçu d’expérience de gestion de capacité hello dans le panneau de gestion de capacité hello.
- Vous pouvez maintenant utiliser des données de diagnostic hello Azure Diagnostics extension toogather à vos machines virtuelles.  La capture de ces données est utile pour analyser les performances des charges de travail et examiner les problèmes.
- Une nouvelle [expérience de déploiement](azure-stack-run-powershell-script.md) remplace les précédents scripts de déploiement par étapes.  nouvelle expérience de déploiement Hello fournit une interface graphique commune par cycle de vie de tout déploiement hello.
- Les comptes Microsoft (MSA) sont désormais pris en charge lors du déploiement.
- L’authentification multifacteur (MFA) est maintenant prise en charge lors du déploiement.  Auparavant, elle devait être désactivée pendant cette opération.

### <a name="known-issues"></a>Problèmes connus
#### <a name="deployment"></a>Déploiement
* Vous remarquerez peut-être que le déploiement prend plus de temps que dans les versions précédentes. 
* Get-AzureStackLogs génère des journaux de diagnostic, toutefois, n’enregistre pas de console toohello de progression.
* Vous devez utiliser hello nouvelles [expérience de déploiement](azure-stack-run-powershell-script.md) toodeploy Azure pile, ou le déploiement risque d’échouer.

#### <a name="portal"></a>Portail
* Vous pouvez voir un tableau de bord vide dans le portail de hello.  Vous pouvez récupérer le tableau de bord hello en sélectionnant hello ENGRENAGE dans le coin supérieur droit de hello du portail de hello et en sélectionnant « Restaurer les paramètres par défaut ».
* Les locataires sont marketplace complète de toobrowse en mesure de hello sans abonnement et seront affiche les éléments d’administration telles que les plans et des offres.  Ces éléments sont tootenants non fonctionnelle.
* Lorsque l’on sélectionne une instance de rôle d’infrastructure, une erreur de référence s’affiche. Hello toorefresh de fonctionnalité d’actualisation du navigateur utilisez hello du portail d’administration.
* bouton « déplacer » de Hello est désactivé sur le panneau de groupe de ressources hello.  Il s’agit du comportement attendu, dans la mesure où le déplacement de groupes de ressources d’un abonnement à l’autre n’est pas pris en charge pour le moment.
* Vous recevrez plusieurs notifications à la fin du téléchargement d’articles de marketplace syndiqués.
* Vous n’êtes pas abonnement de tooyour autorisations tooview en mesure de l’utilisation des portails de pile de Azure hello.  Pour contourner ce problème, vous pouvez vérifier les autorisations avec PowerShell.
* Vous devez ajouter `-TenantID` comme un indicateur lors de l’exportation d’un déploiement terminé comme un script d’automatisation à partir du portail de hello.

#### <a name="services"></a>Services
* Services de coffre de clés doivent être créées à partir du portail de locataires hello ou API client.  Si vous êtes connecté en tant qu’administrateur, vérifiez toocreate portail du locataire hello toouse que les coffres de nouveau le coffre de clés, clés secrètes et les clés.
* Il n’existe aucune expérience de création de groupes de machines virtuelles identiques sur la marketplace, bien qu’il soit possible de le faire avec un modèle.
* Vous ne pouvez pas associer un équilibreur de charge avec un réseau principal via le portail de hello.  Cette tâche peut être effectuée avec PowerShell ou avec un modèle.
* Les groupes de machines virtuelles à haute disponibilité ne sont configurables qu’avec un domaine d’erreur et un domaine de mise à jour chacun de valeur égale à un.  
* Un client doit déjà disposer d’un compte de stockage pour pouvoir créer une nouvelle fonction Azure.
* Machine virtuelle peut échouer et l’état « Impossible de lier argument tooparameter « Carte réseau de l’ordinateur virtuel », car elle est null. »  Réussite du redéploiement de la machine virtuelle de hello.  
* La suppression d’abonnements clients aboutit à des ressources orphelines.  Pour contourner ce problème, supprimez tout d’abord les ressources clientes ou la totalité du groupe de ressources, puis supprimez les abonnements clients. 
* Vous devez créer une règle NAT lors de la création d’un équilibrage de charge réseau, ou vous recevrez une erreur lorsque vous essayez de tooadd une règle NAT après que l’équilibrage de charge hello est créé.
* Les clients peuvent créer des machines virtuelles plus grandes que le quota ne l’autorise.  En effet, les quotas de calcul ne s’appliquent pas.
* Les clients sont hello donné option toocreate un ordinateur virtuel avec stockage géo-redondant.  Cette configuration entraîne toofail de la création d’ordinateur virtuel.
* Peut prendre jusqu'à une heure tooan avant que les clients peuvent créer des bases de données dans un nouveau SQL ou MySQL SKU. 
* La création des éléments directement sur les serveurs qui ne sont pas effectuées par le fournisseur de ressources hello d’hébergement MySQL et SQL n’est pas prise en charge et peut entraîner l’état ne correspondent pas.
* AzureRM PowerShell 1.2.10 requiert des étapes de configuration supplémentaires :
    * Exécutez cette commande après avoir lancé Add-AzureRMEnvironment pour les déploiements Azure AD.  Fournir des valeurs nom et GraphAudience hello à l’aide de la sortie de hello de `Add-AzureRMEnvironment`.
      
      ```PowerShell
      Set-AzureRmEnvironment -Name <Environment Name> -GraphAudience <Graph Endpoint URL>
      ```
    * Exécutez cette commande après avoir lancé Add-AzureRMEnvironment pour les déploiements AD FS.  Fournir des valeurs nom et GraphAudience hello à l’aide de la sortie de hello de `Add-AzureRMEnvironment`.
      
      ```PowerShell
      Set-AzureRmEnvironment <Environment Name> -GraphAudience <Graph Endpoint URL> -EnableAdfsAuthentication:$true
      ```
    
    Par exemple, suivant de hello est utilisé pour un environnement Azure AD :

    ```PowerShell
      Set-AzureRmEnvironment AzureStack -GraphAudience https://graph.local.azurestack.external/
    ```

#### <a name="fabric"></a>Structure
* fournisseur de ressources de calcul Hello affiche un état inconnu.
* adresse IP BMC Bonjour modèle ne sont pas affichés dans des informations essentielles hello d’un nœud d’unité d’échelle.  Ce comportement est attendu dans le kit de développement Azure Stack.
* action de redémarrage Hello sur le rôle d’infrastructure de contrôleur calcul (instance AzS-XRP01) ne doit pas être utilisée.
* Hello Infrastructure panneau sauvegarde ne doit pas être utilisé.
