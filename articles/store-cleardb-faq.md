---
title: "aaaFAQ pour les bases de données ClearDB MySql avec Azure App Service | Documents Microsoft"
description: "Toocommon réponses aux questions sur l’utilisation de bases de données ClearDB MySQL avec Azure App Service."
documentationcenter: php
services: 
author: sunbuild
manager: yochayk
editor: 
tags: mysql
ms.assetid: c2ed5e78-6d7d-4d0c-b7ee-a52ae41ceab8
ms.service: multiple
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/27/2016
ms.author: sumuth
ms.openlocfilehash: 3d9c9daca2b845ede8d3a1fdadefa7e668d62dee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="faq-for-cleardb-mysql-databases-with-azure-app-service"></a>FAQ sur les bases de données MySQL ClearDB avec Azure App Service
Ce FAQ répond aux questions courantes sur l’utilisation et l’achat de bases de données MySQL ClearDB pour Azure Web Apps.

## <a name="what-options-do-i-have-for-mysql-on-azure"></a>Quelles sont les options MySQL sur Azure ?
Vous disposez de plusieurs options :

* [Base de données MySQL partagée ClearDB](/marketplace/partners/cleardb/databases/)
* [Clusters Premium MySQL ClearDB](/marketplace/partners/cleardb-clusters/cluster/)
* [Cluster MySQL s’exécutant sur une machine virtuelle Azure](https://github.com/azure/azure-quickstart-templates/tree/master/mysql-replication)
* [Instance unique de MySQL s’exécutant sur une machine virtuelle Azure](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

ClearDB est un service d’hébergement MySQL et gère l’infrastructure de MySQL hello pour vous. Lorsque vous exécutez votre propre cluster MySQL ou une base de données sur une Machine virtuelle de Azure, vous avez tooset serveur MySQL de hello et qu’il soit mis à jour avec les correctifs.

## <a name="do-i-need-a-credit-card-for-hello-web-app--mysql-template-in-hello-azure-marketplace"></a>Ai-je besoin une carte de crédit pour l’application Web hello + modèle MySQL Bonjour Azure Marketplace ?
Cela dépend de type hello d’abonnement que vous utilisez. Voici quelques types d’abonnement couramment utilisés :

* [Paiement à l’utilisation](/offers/ms-azr-0003p/) : exige une carte de crédit. Quand vous achetez une base de données MySQL payante, votre carte de crédit est débitée.
* [Essai gratuit](https://azure.microsoft.com/pricing/free-trial/) : inclut des crédits à utiliser avec des services Microsoft Azure mais ne permet pas d’acheter des ressources tierces. toopurchase des services tiers ou une base de données MySQL payant, vous devez toouse une carte de crédit, abonnement est activée. Pour Web Apps, vous pouvez créer une base de données MySQL ClearDB GRATUITE.
* [Abonnement MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits/) et **MSDN développement Test paiement**: tooFree similaire d’évaluation, un abonnement MSDN requiert que vous toohave un toopurchase de carte de crédit une solution payante de MySQL de ClearDB.
* [Contrat Entreprise](https://azure.microsoft.com/pricing/enterprise-agreement/) : les clients Contrat Entreprise sont facturés conformément à leur contrat, tous les trimestres, à hauteur de tous leurs achats Azure Marketplace (tiers) sur une facture distincte et cumulée. Vous êtes facturé en dehors de l’engagement de hello pour les achats dans marketplace. Notez que, à ce stade, le magasin Azure n’est pas disponible toocustomers inscrits dans Azerbaïdjan, Croatie, Norvège et Porto Rico. 
* [DreamSpark](https://www.dreamspark.com/Product/Product.aspx?productid=99): vous pouvez créer uniquement des bases de données ClearDB GRATUITES pour Web Apps. Il n’existe aucune limite du nombre de hello des bases de données MySQL de ClearDB gratuit que vous pouvez créer. Notez que les bases de données libres ne sont pas toobe utilisé pour les applications web de production, que ce service a été conçu uniquement pour la version d’évaluation.

## <a name="why-was-i-charged-350-for-a-web-app--mysql-from-hello-azure-marketplace"></a>Pourquoi ai-je été facturé 3,50 USD pour une application Web + MySQL à partir de hello Azure Marketplace ?
option de base de données par défaut Hello est Titan, ce qui est de 3,50 €. Nous ne plus afficher le coût de hello lors de la création de base de données, et vous pouvez acheter par erreur une base de données que vous n’avez l’intention. Nous essayons toofind une expérience de hello tooimprove moyen mais en attendant, vous devez vérifier tous vos niveaux de tarification sélectionnés pour l’application web et de la base de données avant de cliquer sur **créer** et démarrage du déploiement hello des ressources de hello.

## <a name="i-am-running-mysql-on-my-own-azure-virtual-machine-can-i-connect-my-azure-web-app-toomy-database"></a>J’exécute MySQL sur ma propre machine virtuelle Azure. Puis-je connecter ma base de données Azure web app toomy ?
Oui. Vous pouvez vous connecter à votre base de données web application tooyour tant que votre machine virtuelle Azure a donné accès à distance tooyour web app. Pour plus d’informations, consultez la page [Installer MySQL sur une machine virtuelle](virtual-machines/windows/classic/mysql-2008r2.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="in-which-countries-are-cleardb-premium-mysql-clusters-supported"></a>Dans quels pays les clusters Premium MySQL ClearDB sont-ils pris en charge ?
[Les clusters ClearDB Premium MySQL](/marketplace/partners/cleardb-clusters/cluster/) sont disponibles dans toutes les régions Azure dans le monde à l’exception de hello de l’Inde, Australie, Brésil Sud et en Chine.

## <a name="can-i-create-a-new-cluster-prior-toocreating-a-database-with-cleardb-premium-cluster-solution"></a>Puis-je créer un nouveau toocreating préalable de cluster une base de données avec la solution de cluster ClearDB premium ?
Non, la création de clusters ClearDB vides n’est pas prise en charge. Hello portail Azure vous permet de bases de données toocreate dans un cluster, ce qui peut créer un nouveau cluster à hello même temps.

## <a name="will-i-be-warned-if-i-try-toodelete-a-cleardb-mysql-database-that-is-in-use-by-one-of-my-applications"></a>J’ai indiquera si vous essayez de toodelete une base de données ClearDB MySQL est en cours d’utilisation par un de mes applications ?
Non, Azure ne vous avertit pas si vous supprimez un achat Marketplace dont dépend votre application.

## <a name="which-regions-can-i-create-cleardb-databases-in"></a>Dans quelles régions puis-je créer des bases de données ClearDB ?
Azure Marketplace n’est pas disponible toocustomers inscrits dans Azerbaïdjan, Croatie, Norvège ou Porto Rico. ClearDB n’est pas disponible dans ces régions.

## <a name="what-pricing-tier-should-i-choose-for-a-production-web-app-and-database"></a>Quel niveau tarifaire dois-je choisir pour une application web de production et une base de données ?
Utilisez le niveau tarifaire De base ou un niveau supérieur pour Web Apps. Pour ClearDB, nous vous recommandons d’utiliser un plan Saturne ou Jupiter. Passez en revue les fonctionnalités de hello et limitations de chaque niveau de tarification pour les deux [Web Apps](https://azure.microsoft.com/pricing/details/app-service/) et [bases de données ClearDB MySQL](/marketplace/partners/cleardb/databases/) hello toochoose qui correspond à vos besoins.

## <a name="how-do-i-upgrade-my-cleardb-database-from-one-plan-tooanother"></a>Comment mettre à niveau ma base de données ClearDB à partir d’un plan tooanother ?
Bonjour [portail Azure](https://portal.azure.com), vous pouvez monter une base de données d’hébergement partagé de ClearDB. Lire ce [article](https://blogs.msdn.microsoft.com/appserviceteam/2016/10/06/upgrade-your-cleardb-mysql-database-in-azure-portal/) toolearn plus. Nous n’actuellement en charge mise à niveau pour les clusters ClearDB Premium Bonjour portail Azure.

## <a name="i-cant-see-my-cleardb-database-in-azure-portal"></a>Ma base de données ClearDB ne s’affiche pas dans le portail Azure.
Si nous créons la base de données ClearDB à l’aide du Gestionnaire de ressources Azure ou [nouveau portail Azure](https://portal.azure.com), il ne sera pas visible dans hello [ancien portail Azure](https://manage.windowsazure.com). toowork-contourner ce problème est toolink votre base de données manuellement l’application web toohello. Même si créer la base de données ClearDB Bonjour [ancien portail](https://manage.windowsazure.com) à ne pas être en mesure de toosee votre base de données hello [nouveau portail Azure](https://portal.azure.com). Il n’existe aucune solution de contournement pour un scénario de ce dernier hello.

## <a name="who-do-i-contact-for-support-when-my-database-is-down"></a>Qui dois-je contacter pour obtenir de l’aide quand ma base de données est en panne ?
Contactez le [support ClearDB](https://www.cleardb.com/developers/help/support) pour tout problème lié à la base de données. Tooprovide de préparer les informations d’abonnement Azure.

## <a name="can-i-create-additional-users-for-my-cleardb-mysql-database-cluster-solution"></a>Puis-je créer des utilisateurs supplémentaires pour ma solution de cluster de base de données ClearDB MySQL ?
Non. Vous ne pouvez pas créer des utilisateurs supplémentaires, mais vous pouvez créer des bases de données sur votre cluster de base de données ClearDB.  

## <a name="can-basicpro-series-databases-be-upgraded-in-place-similar-tooplanetary-plans-today-on-cleardb-portal"></a>Bases de données de série Basic/Pro peuvent être des mises à niveau sur place similaire tooPlanetary plans aujourd'hui sur ClearDB portail ?
Oui, les bases de données Basic peuvent être mises à niveau sur place (Basic 60 à Basic 500). Les bases de données Pro peuvent être mises à niveau sur place (Pro 125 à Pro 1000), à l’exception de Pro 60. Actuellement, nous ne prenons pas en charge la mise à niveau de la base de données Pro 60. 

## <a name="when-i-migrate-my-resources-from-one-subscription-tooanother-does-my-cleardb-mysql-database-get-migrated-as-well"></a>Lorsque mes ressources migrer à partir d’un abonnement tooanother, ma base de données ClearDB MySQL obtenir également migré ?
Lorsque vous effectuez la migration de ressources entre les différents abonnements, certaines [limitations](app-service-web/app-service-move-resources.md) s’appliquent. Une base de données ClearDB MySQL est un service tiers et ne peut donc pas être migrée lors d’une migration d’abonnement Azure. Si vous ne gérez pas la migration de votre MySQL hello toomigrating préalable Azure de base de données des ressources, votre MySQL de ClearDB bases de données peuvent être désactivés. Commencez par migrer manuellement vos bases de données, puis effectuez la migration des abonnements Azure pour votre application web. 

## <a name="i-hit-hello-spending-limit-on-my-subscription-i-removed-hello-limit-and-my-app-service-is-online-however-hello-database-is-not-accessible-how-do-i-re-enable-hello-cleardb-database"></a>J’a atteint la limite de dépense de mon abonnement de hello. J’ai supprimé la limite de hello et mon application de Service est en ligne, mais la base de données hello n’est pas accessible. Comment ré-activer base de données ClearDB hello ?
Contact [prise en charge ClearDB](https://www.cleardb.com/developers/help/support) base de données toore-enable hello. Préparez-vous à fournir les informations sur votre abonnement Azure et le nom de la base de données.

## <a name="can-i-transfer-a-cleardb-database-from-a-credit-card-subscription-tooan-ea-subscription"></a>Puis-je transférer une base de données ClearDB à partir d’un carte de crédit abonnement tooan EA abonnement ?
Bases de données ClearDB utilisent hello carte de crédit associée à des abonnements existants hello. toouse un abonnement EA vous devez toomigrate vos données tooa nouvelle base de données :

* Achetez une nouvelle base de données ClearDB avec votre abonnement Contrat Entreprise.
* Migrer vos données tooyour nouvelle base de données.
* Mettre à jour votre application toouse hello nouvelle base de données.
* Supprimez votre ancienne base de données ClearDB.

Lorsque vous créez une application web avec MySQL (ClearDB) ou que vous créez une base de données MySQL (ClearDB), hello abonnement que vous choisissez détermine la façon dont vous allez payer pour le service de hello. Avec un abonnement EA, nous ne bloquera pas d’approvisionnement de hello de hello des services tiers tels que ClearDB Bonjour portail Azure. Les abonnements Contrat Entreprise sont facturés hors engagement monétaire, tous les trimestres et à terme échu. client EA Hello aurait tooset un mode de paiement comme un toopay de carte de crédit pour tous les services tiers marketplace.

## <a name="where-can-i-see-hello-charges-for-cleardb-resources-in-an-ea-subscription"></a>Où puis-je voir frais hello pour les ressources ClearDB dans un abonnement EA ?
Pour les clients EA directe, les frais d’Azure Marketplace sont visibles sur hello Enterprise Portal. Notez que tous les achats et consommations Marketplace sont facturés hors engagement monétaire, tous les trimestres et à terme échu. Les clients EA ont toopay directement peut et fournisseurs de service tiers toohello ne prennent donc en activant le mode de paiement, tel qu’une carte de crédit avec leur EA en compte.

Les clients EA indirects trouverez leurs abonnements Azure Marketplace sur hello **gérer les abonnements** page hello portail d’entreprise, mais la tarification est masquée. Les clients doivent contacter leur fournisseur de services de concession de licences (LSP) pour obtenir des informations sur les frais Marketplace.

Accès tooAzure Marketplace pour les services tiers peut être géré par les administrateurs de l’inscription EA Azure. Ils peuvent désactiver ou réactiver l’accès too3rd tiers achats hello magasin dans Gestion des comptes et des abonnements sous la section des comptes hello Bonjour Enterprise Portal.

## <a name="who-do-i-contact-for-questions-about-my-bill-for-cleardb-services-in-my-ea-subscription"></a>Qui dois-je contacter pour toute question sur ma facture des services ClearDB dans mon abonnement Contrat Entreprise ?
Contact [prise en charge du client Enterprise](http://aka.ms/AzureEntSupport) avec toobilling ce qui concerne les sous leur inscription EA. Hello équipe de Support Portal EA répondront à votre question ou aider à résoudre votre problème.

## <a name="more-information"></a>Plus d’informations
[FAQ Azure Marketplace](/marketplace/faq/)

