---
title: "aaaLog Analytique des fonctionnalités pour les fournisseurs de Service | Documents Microsoft"
description: "Log Analytics permet aux fournisseurs de services gérés (MSP), grandes entreprises, éditeurs de logiciels indépendants (ISV) et fournisseurs de service d’hébergement de gérer et de surveiller les serveurs situés dans l’infrastructure locale ou cloud d’un client."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: c07f0b9f-ec37-480d-91ec-d9bcf6786464
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/22/2016
ms.author: richrund
ms.openlocfilehash: 3c0a93232293f90385c6c724be436cee1cf855f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-features-for-service-providers"></a>Fonctionnalités de Log Analytics pour les fournisseurs de services
Log Analytics permet aux fournisseurs de services gérés (MSP), grandes entreprises, éditeurs de logiciels indépendants (ISV) et fournisseurs de service d’hébergement de gérer et de surveiller les serveurs situés dans l’infrastructure locale ou cloud d’un client. 

Les grandes entreprises et les fournisseurs de services présentent de nombreux points communs, en particulier si les ressources informatiques de plusieurs divisions sont gérées par une équipe informatique centralisée. Par souci de simplicité, ce document utilise le terme de hello *fournisseur de services* mais hello même fonctionnalité est également disponible pour les entreprises et d’autres clients.

## <a name="cloud-solution-provider"></a>Fournisseur de solutions cloud
Pour les partenaires et fournisseurs de services qui font partie de hello [fournisseur de solutions de Cloud (CSP)](https://partner.microsoft.com/Solutions/cloud-reseller-overview) du programme, Analytique de journal est un de hello Azure services disponibles sur un abonnement du fournisseur de services cryptographiques. 

Pour l’Analytique des journaux, hello suivant les fonctionnalités est activée dans *fournisseur de solutions de Cloud* abonnements.

En tant que *fournisseur de solutions cloud*, vous pouvez :

* Créer des espaces de travail Log Analytics dans l’abonnement d’un client.
* Accéder aux espaces de travail créés par des clients. 
* Ajouter et supprimer l’espace de travail toohello de l’accès utilisateur à l’aide de la gestion des utilisateurs d’Azure. Lorsque dans l’espace de travail d’un locataire hello OMS la page de gestion hello portail utilisateur sous paramètres n’est pas disponible
  * Analytique de journal ne prend pas en charge l’accès en fonction du rôle encore - attribution à un utilisateur `reader` Bonjour portail Azure permet les modifications de configuration toomake dans portail OMS : hello

toolog dans tooa l’abonnement du client, vous devez identificateur du locataire toospecify hello. Identificateur du locataire Hello est souvent cette dernière partie de hello messagerie adresse utilisée toosign dans.

* Dans le portail OMS : hello, ajoutez `?tenant=contoso.com` dans l’URL de hello pour le portail de hello. Par exemple, `mms.microsoft.com/?tenant=contoso.com`
* Dans PowerShell, utilisez hello `-Tenant contoso.com` paramètre lors de l’utilisation `Add-AzureRmAccount` applet de commande
* Identificateur du locataire Hello est automatiquement ajouté lorsque vous utilisez hello `OMS portal` lien du hello tooopen portail Azure et connectez-vous au portail OMS est toohello pour l’espace de travail hello sélectionné

En tant que *client* d’un fournisseur de solutions cloud, vous pouvez :

* Créer des espaces de travail Log Analytics dans un abonnement CSP.
* Espaces de travail Access créés par hello CSP
  * Hello d’utilisation `OMS portal` lien du hello tooopen portail Azure et connectez-vous au portail OMS est toohello pour l’espace de travail hello sélectionné
* Afficher et utiliser la page de gestion d’utilisateur hello sous paramètres dans portail OMS : hello

> [!NOTE]
> Hello sauvegarde et les solutions de récupération de Site pour l’Analytique des journaux ne sont pas en mesure de tooconnect tooa Services de récupération coffre ne peut pas être configurées dans un abonnement du fournisseur de services cryptographiques. 
> 
> 

## <a name="managing-multiple-customers-using-log-analytics"></a>Gestion de plusieurs clients à l’aide de Log Analytics
Nous vous recommandons de créer un espace de travail Log Analytics pour chaque client que vous gérez. Un espace de travail Log Analytics offre :

* Un emplacement géographique pour toobe des données stockée. 
* des données granulaires pour la facturation ; 
* l’isolation des données. 
* une configuration unique.

En créant un espace de travail par client, vous tookeep en mesure de données de chaque client distinctes et également suivre l’utilisation de hello de chaque client.

Plus d’informations sur quand et pourquoi toocreate plusieurs espaces de travail est décrit dans [gérer l’accès toolog analytique](log-analytics-manage-access.md#determine-the-number-of-workspaces-you-need).

Création et configuration des espaces de travail client peuvent être automatisées à l’aide de [PowerShell](log-analytics-powershell-workspace-configuration.md), [modèles Resource Manager](log-analytics-template-workspace-configuration.md), ou à l’aide de hello [API REST](https://www.nuget.org/packages/Microsoft.Azure.Management.OperationalInsights/).

utilisation de Hello de modèles du Gestionnaire de ressources pour la configuration de l’espace de travail vous permet de toohave un modèle de configuration qui peuvent être utilisé toocreate et configurer les espaces de travail. Vous pouvez être certain que les espaces de travail sont créés pour les clients qu’ils sont automatiquement configuré tooyour exigences. Lorsque vous mettez à jour vos exigences, modèle de hello est mise à jour et puis réappliqué les espaces de travail existants hello. Grâce à ce processus, même les espaces de travail existants répondent à vos nouvelles normes.    

Lorsque vous gérez plusieurs espaces de travail Analytique de journal, nous vous recommandons d’intégration de chaque espace de travail à votre système de tickets existant / à l’aide de la console Opérateur hello [alertes](log-analytics-alerts.md) fonctionnalité. Grâce à l’intégration avec vos systèmes existants, personnel du support peut continuer toofollow leurs processus familiers. Analytique de journal vérifie chaque espace de travail par rapport aux critères d’alerte hello que vous spécifiez régulièrement et génère une alerte lorsqu’une action est requise.

Pour obtenir des vues personnalisées de données, utilisez hello [tableau de bord](../azure-portal/azure-portal-dashboards.md) fonctionnalité Bonjour portail Azure.  

Niveau exécutif de rapports qui résument les données entre les espaces de travail que vous pouvez utiliser hello intégration entre Analytique de journal et [PowerBI](log-analytics-powerbi.md). Si vous avez besoin de toointegrate avec un autre système de création de rapports, vous pouvez utiliser les API de recherche de hello (via PowerShell ou [reste](log-analytics-log-search-api.md)) toorun requêtes et l’exportation des résultats de recherche.

## <a name="next-steps"></a>Étapes suivantes
* Automatiser la création et la configuration des espaces de travail à l’aide de [modèles Resource Manager](log-analytics-template-workspace-configuration.md)
* Automatiser la création des espaces de travail à l’aide de [PowerShell](log-analytics-powershell-workspace-configuration.md) 
* Utilisez [alertes](log-analytics-alerts.md) toointegrate avec les systèmes existants
* Générer des rapports de synthèse à l’aide de [PowerBI](log-analytics-powerbi.md)

