---
title: "tooAzure de données de l’utilisation de Azure pile aaaReport | Documents Microsoft"
description: "Découvrez comment tooset des données d’utilisation de création de rapports dans la pile de Azure."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun;AlfredoPizzirani
ms.openlocfilehash: deecd66d9022b2e0c274ff4e0276d3b2e3bcc99e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="report-azure-stack-usage-data-tooazure"></a>TooAzure de pile Azure l’utilisation des données de rapport 

Données d’utilisation, également appelées comme données de consommation représentent la quantité hello de ressources utilisées. Dans la pile d’Azure, l’utilisation de données doivent être signalée tooAzure pour but de facturation. Administrateurs de cloud Azure pile doivent configurer leur tooAzure de données Azure pile instance tooreport d’utilisation.

> [!NOTE]
> Rapport d’utilisation des données n’est pas obligatoire pour hello Kit de développement de pile Azure, et les utilisateurs ne sont pas facturés pour la consommation des ressources. Toutefois, les administrateurs de cloud Azure Stack peuvent tester cette fonctionnalité et faire part de commentaires la concernant. Lorsque plusieurs nœuds de pile de Azure est généralement disponible, tous les environnements de plusieurs nœuds hello doivent signaler tooAzure des données d’utilisation.

![flux de facturation](media/azure-stack-usage-reporting/billing-flow.png)

Les données d’utilisation sont envoyées à partir de tooAzure Azure pile via hello pont Azure. Dans Azure, le processus de système de commerce de hello hello des données d’utilisation et génère la facture de hello. Après la génération de la facture de hello, propriétaire de l’abonnement Azure hello peut afficher et télécharger à partir de hello [centre des comptes Azure](https://account.windowsazure.com/Subscriptions). toolearn sur la pile de Azure est concédé sous licence, consultez toohello [pile Azure packaging et la tarification de document](https://go.microsoft.com/fwlink/?LinkId=842847&clcid=0x409).

## <a name="set-up-usage-data-reporting"></a>Configurer la génération de rapports de données d’utilisation

tooset des données d’utilisation de création de rapports dans la pile d’Azure, vous devez [enregistrer votre instance de la pile d’Azure avec Azure](azure-stack-register.md). Dans le cadre du processus d’inscription de hello, pile de Azure est configuré avec hello pont Azure, qui se connecte à Azure pile tooAzure et envoie les données d’utilisation hello. Hello les données d’utilisation suivantes est envoyée à partir de la pile de Azure tooAzure :

* **Contrôler les ID** : ID Unique pour la ressource hello qui a été consommée.
* **Quantité** : quantité de données d’utilisation de ressources qui s’est produite au cours d’une période déterminée.
* **Emplacement** – emplacement où les ressources Azure pile actuelle hello sont déployé.
* **URI de ressource** – complet des URI de ressource hello pour lequel l’utilisation est signalée. 
* **ID d’abonnement** – ID d’abonnement de l’utilisateur d’Azure pile hello.
* **Temps** – heure de début et de fin des données d’utilisation de hello. Il existe un certain délai entre temps hello lorsque ces ressources sont consommées dans la pile d’Azure et lorsque les données d’utilisation hello sont signalé toocommerce. Pile Azure regroupe les données d’utilisation pour toutes les 24 heures et toocommerce des données d’utilisation de reporting pipeline dans Azure prend une autre quelques heures. C’est le cas, l’utilisation de qui se produit juste avant minuit susceptibles d’apparaître dans Azure hello suivant jour.

## <a name="test-usage-data-reporting"></a>Tester la génération de rapports de données d’utilisation 

1. Création de rapports, les données d’utilisation tootest créer quelques ressources dans la pile d’Azure. Par exemple, vous pouvez créer un [compte de stockage](azure-stack-provision-storage-account.md), [machine virtuelle Windows Server](azure-stack-provision-vm.md) et un VM Linux avec toosee Basic et les références (SKU) Standard, comment l’utilisation des cœurs est signalée. données d’utilisation Hello pour différents types de ressources sont signalées sous différents compteurs.  

2. Laissez vos ressources s’exécuter pendant quelques heures. Les informations d’utilisation sont collectées environ une fois par heure. Après avoir recueilli, ces données sont tooAzure transmise et traitées dans hello système commerce Azure. Ce processus peut prendre tooa quelques heures.  

3. Connectez-vous à toohello [centre des comptes Azure](https://account.windowsazure.com/Subscriptions) comme hello Azure compte administrateur et sélectionnez hello abonnement Azure que vous avez utilisé tooregister hello Azure pile. Vous pouvez afficher les données d’utilisation de pile de Azure hello, quantité hello facturée pour chaque hello utilisé des ressources comme indiqué dans hello suivant image :  
   ![flux de facturation](media/azure-stack-usage-reporting/pricng-details.png)

Pour hello Kit de développement de pile Azure, les ressources de Azure pile ne sont pas facturées ainsi, le prix de hello est affiché comme 0,00 $. Lorsque plusieurs nœuds de pile de Azure est généralement disponible, vous pouvez voir hello réelle de coût pour chacun de ces ressources. 

## <a name="which-azure-stack-instances-are-charged"></a>Quelles sont les instances Azure Stack facturées ?
L’utilisation de ressources est gratuite pour les instances du Kit de développement Azure Stack. 

Disponibilité générale, les systèmes à plusieurs nœuds Azure pile sont facturés alors que l’environnement de kit de développement hello reste disponible sans frais supplémentaires. Pour les systèmes à plusieurs nœuds, les machines virtuelles de charge de travail, les services de stockage et App Services sont facturés. 

## <a name="are-users-charged-for-hello-infrastructure-vms"></a>Les utilisateurs sont facturés pour l’infrastructure hello machines virtuelles ?
Non, les données d’utilisation hello pour l’infrastructure Azure pile machines virtuelles, qui sont créés au cours du déploiement sont signalé tooAzure, mais pas de frais pour ces machines virtuelles. infrastructure de Hello machines virtuelles comprennent des machines virtuelles hello qui sont créés par le script de déploiement Azure pile hello et hello machines virtuelles qui s’exécutent comme des fournisseurs de ressources de tiers de Microsoft de calcul, stockage, SQL.

## <a name="what-azure-meters-are-used-when-reporting-usage-data"></a>Quels compteurs Azure sont utilisés lors du signalement de données d’utilisation ?
Hello Voici hello deux ensembles de compteurs qui sont utilisés dans les rapports de données d’utilisation :  

* **Compteurs du prix total** : utilisés pour les ressources associées à des charges de travail utilisateur.  
* **Compteurs d’administration** : utilisés pour les ressources d’infrastructure. Ces compteurs ont un prix de zéro dollar.

## <a name="which-subscription-is-charged-for-hello-resources-consumed"></a>Abonnement est facturé pour la consommation des ressources hello ?
Hello d’abonnement est fourni lorsque [l’inscription de la pile d’Azure avec Azure](azure-stack-register.md) est facturé.

## <a name="what-types-of-subscriptions-are-supported-for-usage-data-reporting"></a>Quels types d’abonnements sont pris en charge pour la génération de rapports de données d’utilisation ?
Pour les abonnements de Kit de développement Azure pile, accord entreprise (EA), paiement à l’utilisation et MSDN hello prend en charge les rapports de données d’utilisation. 

## <a name="does-usage-data-reporting-work-in-sovereign-clouds"></a>La génération de rapports de données d’utilisation fonctionne-t-elle avec les clouds souverains ?
Dans le Kit de développement Azure pile de hello, rapport d’utilisation des données requiert des abonnements qui sont créés dans le système global Azure hello. Les abonnements créés dans un des clouds de souverains hello (clouds hello Azure Government Azure situés en Allemagne et Azure Chine) ne peut pas être inscrit dans Azure, afin qu’ils ne prennent pas en charge les rapports de données d’utilisation. 

## <a name="can-an-administrator-test-usage-data-reporting-before-ga"></a>Un administrateur peut-il tester la génération de rapports de données d’utilisation avant la mise à disposition générale ?
Oui, les administrateurs de pile de Azure peuvent tester hello d’utilisation des rapports de données par [inscription](azure-stack-register.md) instance de kit de développement hello avec Azure. Une fois inscrit, les données d’utilisation démarre circulant de votre tooyour d’instance Azure pile abonnement Azure. 

## <a name="how-can-users-identify-azure-stack-usage-data-in-hello-azure-billing-portal"></a>Comment les utilisateurs peuvent identifier les données d’utilisation Azure pile Bonjour Azure portail de facturation ?
Les utilisateurs peuvent voir les données d’utilisation Azure pile hello dans le fichier des informations sur l’utilisation hello. tooknow sur la façon dont l’utilisation de hello tooget détails fichier, consultez toohello [télécharger le fichier d’utilisation de hello centre des comptes Azure](../billing/billing-download-azure-invoice-daily-usage-date.md#download-usage-from-the-account-center-csv) l’article. fichier des informations sur l’utilisation Hello contient des compteurs de pile de Azure hello qui identifient le stockage de la pile d’Azure et les machines virtuelles. Toutes les ressources utilisées dans la pile de Azure sont signalées sous la région de hello nommée « Pile Azure ».

## <a name="why-doesnt-hello-usage-reported-in-azure-stack-match-hello-report-generated-from-azure-account-center"></a>Pourquoi l’utilisation de hello n’a signalé dans Azure pile correspondent aux rapports hello généré à partir du centre de compte Azure ?
Il existe un décalage entre lorsque les données d’utilisation hello sont générées dans la pile d’Azure et lorsqu’il est soumis tooAzure commerce. délai de Hello est hello durée tooupload données d’utilisation de commerce tooAzure de pile de Azure. En raison du délai de toothis, d’utilisation qui se produit dans quelques instants avant minuit peut apparaissent dans Azure hello suivant jour. Si vous utilisez hello [API de l’utilisation de pile Azure](azure-stack-provider-resource-api.md)et les résultats de hello toohello utilisation indiquée dans la comparaison hello portail de facturation Azure, vous pouvez voir une différence.

## <a name="next-steps"></a>Étapes suivantes

* [API d’utilisation du fournisseur](azure-stack-provider-resource-api.md)  
* [API d’utilisation du locataire](azure-stack-tenant-resource-usage-api.md)
* [Forum Aux Questions sur l’utilisation](azure-stack-usage-related-faq.md)