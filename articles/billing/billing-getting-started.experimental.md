---
title: "aaaPrevent inattendue des coûts, gérez la facturation - Azure | Documents Microsoft"
description: "Découvrez comment tooavoid frais inattendues sur votre facture Azure. Utilisez les fonctionnalités de gestion et de suivi des coûts pour un abonnement Microsoft Azure."
services: 
documentationcenter: 
author: tonguyen10
manager: tonguyen
editor: 
tags: billing
ms.assetid: 482191ac-147e-4eb6-9655-c40c13846672
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: tonguyen
ms.openlocfilehash: d380f27861531351ac8e570469c59a84b9ca99e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prevent-unexpected-charges-with-azure-billing-and-cost-management"></a>Éviter les charges inattendues avec la gestion de la facturation et des coûts dans Azure

Lorsque vous vous inscrivez pour Azure, il existe plusieurs possibilités tooget une meilleure idée de votre dépense. Hello [calculatrice de prix](https://azure.microsoft.com/pricing/calculator/) peut fournir une estimation des coûts avant de créer une ressource Azure. Hello [portail Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) vous offre de répartition des coûts hello actuelle et de prévision pour votre abonnement. Si vous souhaitez toogroup et comprenez les coûts pour différents projets ou les équipes, examinez [ressource marquage](../azure-resource-manager/resource-group-using-tags.md). Si votre organisation dispose d’un système de création de rapports que vous préférez toouse, consultez hello [facturation API](billing-usage-rate-card-overview.md). 

Vous pouvez également [télécharger les factures précédentes et décrit en détail les fichiers d’utilisation](billing-download-azure-invoice-daily-usage-date.md) toomake que vous avez été facturé correctement. Pour plus d’informations sur la relation entre votre facture et votre utilisation quotidienne, consultez [Comprendre votre facture Microsoft Azure](billing-understand-your-bill.md).

Si votre abonnement est via un contrat entreprise (EA), fournisseur de solutions de Cloud (CSP) ou sponsoring Azure, de nombreuses fonctionnalités dans cet article ne s’appliquent tooyou. Au lieu de cela, nous avons un autre ensemble d’outils que vous pouvez utiliser pour la gestion des coûts. Consultez [Ressources supplémentaires pour les offres EA, CSP et Sponsorship](#other-offers).

Si votre abonnement est une évaluation gratuite, [Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/), Azure dans Open (AIO) ou BizSpark, votre abonnement sera automatiquement désactivé lorsque tous vos crédits sont utilisés. En savoir plus sur [limites de dépense](#spending-limit) tooavoid votre abonnement unexpectantly désactivé. 

## <a name="get-estimated-costs-before-adding-azure-services"></a>Obtenir les coûts estimés avant d’ajouter des services Azure

### <a name="estimate-cost-online-using-hello-pricing-calculator"></a>Estimer le coût en ligne à l’aide de calculatrice de prix hello

Extraire hello [calculatrice de prix](https://azure.microsoft.com/pricing/calculator/) tooget coût estimé mensuel du service hello vous intéresse. Vous pouvez ajouter n’importe quel tooget ressource Azure de première partie une estimation de coût.

![Capture d’écran de menu de la calculatrice de tarification de hello](./media/billing-getting-started/pricing-calc.png)

Par exemple, une Machine virtuelle Windows de A1 (VM) est estimée toocost 66.96 USD/mois de calcul heures si vous laisser toute exécution hello :

![Capture d’écran de la calculatrice de prix hello indiquant qu’une machine virtuelle Windows de A1 est estimé toocost 66.96 dollars par mois](./media/billing-getting-started/pricing-calcVM.png)

Pour plus d’informations sur les prix, reportez-vous à cette [FAQ](https://azure.microsoft.com/pricing/faq/). Ou, si vous souhaitez tootalk tooan vendeur Azure, contactez 1-800-867-1389.

### <a name="review-hello-estimated-cost-in-hello-azure-portal"></a>Hello de révision estimation du coût Bonjour portail Azure

En général, lorsque vous ajoutez un service Bonjour portail Azure, il est un affichage qui vous présente un coût estimé similaires par mois. Par exemple, lorsque vous choisissez la taille de hello de votre machine virtuelle Windows, vous voyez hello estimé mensuelle pour les heures de calcul hello :

![Exemple : une machine virtuelle Windows de A1 est estimé toocost 66.96 dollars par mois](./media/billing-getting-started/vm-size-cost.PNG)

### <a name="set-up-billing-alerts"></a>Configurer des alertes de facturation

Définir des alertes de facturation des messages électroniques tooget lorsque vos coûts d’utilisation dépassent un montant que vous spécifiez. Si vous disposez de crédits mensuels, configurez des alertes pour être averti lorsqu’un montant spécifique a été utilisé. Pour plus d’informations, consultez [Configurer des alertes de facturation pour vos abonnements Microsoft Azure](billing-set-up-alerts.md).

![Capture d’écran d’un e-mail d’alerte de facturation](./media/billing-getting-started/billing-alert.png)

> [!NOTE]
> Cette fonctionnalité étant encore en version préliminaire, il est recommandé de vérifier régulièrement l’utilisation.

Vous souhaiterez peut-être toouse hello estimation des coûts de hello calculatrice de tarification comme une indication de votre première alerte.

### <a name="spending-limit"></a> Vérifiez si la limite de dépense est activée

Si vous avez un abonnement qui utilise des crédits, puis hello limite de dépense est activée pour vous par défaut. De cette manière, lorsque vous dépensez tous vos crédits, votre carte bancaire n’est pas facturée. Consultez hello [la liste complète des offres Azure et disponibilité hello de limite de dépense](https://azure.microsoft.com/support/legal/offer-details/).

Toutefois, si vous atteignez votre limite de dépense, vos services sont désactivés. Cela signifie que vos machines virtuelles sont libérées. tooavoid d’interruption de service, vous devez désactiver hello limite de dépense. Tout dépassement est facturé sur la carte de crédit enregistrée. 

toosee si vous avez obtenu limite de dépense, accédez à toohello [affichage des abonnements Bonjour centre des comptes](https://account.windowsazure.com/Subscriptions). Une bannière s’affiche si votre limite de dépense est activée :

![Capture d’écran qui affiche un avertissement sur la limite en cours sur Bonjour centre des comptes de dépense](./media/billing-getting-started/spending-limit-banner.PNG)

Cliquez sur la bannière de hello et suivez les invites hello de tooremove limite de dépense. Si vous n’avez pas entré les informations de carte de crédit lors de votre inscription, vous devez l’entrer hello tooremove limite de dépense. Pour plus d’informations, consultez [Azure limite de dépense – comment il fonctionne et comment tooenable ou supprimez-le](https://azure.microsoft.com/pricing/spending-limits/).

## <a name="ways-toomonitor-your-costs-when-using-azure-services"></a>Méthodes toomonitor vos coûts lors de l’utilisation des services Azure

### <a name="tags"></a>Ajouter des balises tooyour ressources toogroup vos données de facturation

Vous pouvez utiliser les données de facturation toogroup balises pour les services pris en charge. Par exemple, si vous exécutez plusieurs ordinateurs virtuels pour différentes équipes, vous pouvez utiliser les coûts de balises toocategorize par centre de coût (h, marketing, finance) ou d’environnement (test de préproduction, production). 

![Capture d’écran qui affiche l’affectation des balises dans le portail de hello](./media/billing-getting-started/tags.PNG)

Hello balises s’affichent dans l’ensemble des coûts différentes vues de rapports. Par exemple, elles sont visibles dans votre [vue d’analyse des coûts](#costs) immédiatement et dans le [fichier .csv d’utilisation détaillée](#invoice-and-usage) après votre première période de facturation.

Pour plus d’informations, consultez [à l’aide des balises tooorganize vos ressources Azure](../azure-resource-manager/resource-group-using-tags.md).

### <a name="costs"></a>Régulièrement vérifier portail hello pour la répartition des coûts et taux d’avancement

Une fois que vos services sont actifs, vérifiez régulièrement combien ils vous coûtent. Vous pouvez voir hello actuel dépenses et taux d’avancement dans le portail Azure. 

1. Visitez hello [panneau abonnements dans le portail Azure](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) et sélectionnez un abonnement.

2. Vous devez voir la répartition des coûts hello et taux d’avancement dans le panneau de fenêtre contextuelle hello. Il ne peut pas être pris en charge pour votre offre (un avertissement s’affichera haut hello).

    ![Capture d’écran de taux d’avancement et de répartition Bonjour portail Azure](./media/billing-getting-started/burn-rate.PNG)

3. Cliquez sur **analyse coût** dans hello liste toohello toosee gauche hello répartition des coûts par ressource. Attendez 24 heures après avoir ajouté un service pour hello données toopopulate.

    ![Capture d’écran de la vue d’analyse coût hello dans le portail Azure](./media/billing-getting-started/cost-analysis.PNG)

4. Vous pouvez filtrer les données en fonction de différentes propriétés : [balises](#tags), groupe de ressources, intervalle de temps, etc. Cliquez sur **appliquer** tooconfirm des filtres hello et **télécharger** si vous souhaitez tooexport hello vue tooa Comma-Separated fichier .csv (valeurs).

5. En outre, vous pouvez cliquer sur une ressource toosee passent à l’historique et la quantité des ressources de hello coûte chaque jour.

    ![Capture d’écran de hello passent à l’affichage de l’historique dans le portail Azure](./media/billing-getting-started/costhistory.PNG)

Nous vous recommandons de vérifier les coûts de hello que vous consultez des estimations hello que était affiché lorsque vous avez sélectionné les services hello. Si les coûts de hello diffèrent grandement des estimations, vérifiez hello plan tarifaire (A1 vs machine virtuelle A0, par exemple) que vous avez sélectionné pour vos ressources. 

### <a name="consider-enabling-cost-cutting-features-like-auto-shutdown-for-vms"></a>Envisagez d’activer les fonctionnalités de réduction des coûts telles que l’arrêt automatique pour les machines virtuelles

Selon votre scénario, vous pouvez configurer l’arrêt automatique pour vos machines virtuelles Bonjour portail Azure. Pour en savoir plus, consultez le billet de blog [Auto-shutdown for VMs using Azure Resource Manager](https://azure.microsoft.com/blog/announcing-auto-shutdown-for-vms-using-azure-resource-manager/) (Arrêt automatique des machines virtuelles à l’aide d’Azure Resource Manager).

![Capture d’écran de l’option d’arrêt automatique dans le portail de hello](./media/billing-getting-started/auto-shutdown.PNG)

Arrêt automatique n’est pas hello identique, comme lorsque vous arrêtez dans hello machine virtuelle avec les options d’alimentation. Arrêt automatique s’arrête et libère des frais d’utilisation supplémentaires de votre toostop de machines virtuelles. Pour plus d’informations, consultez les informations concernant les états des machines virtuelles dans le FAQ sur la facturation pour les [machines virtuelles Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/) et les [machines Windows VMs](https://azure.microsoft.com/pricing/details/virtual-machines/windows/).

Pour bénéficier d’autres fonctionnalités de réduction des coûts pour vos environnements de développement et de test, consultez [Azure DevTest Labs](https://azure.microsoft.com/services/devtest-lab/).

### <a name="turn-on-and-check-out-azure-advisor-recommendations"></a>Activez et consultez les recommandations d’Azure Advisor

[Azure Advisor](../advisor/advisor-overview.md) est une fonctionnalité en version préliminaire qui vous permet de réduire les coûts en identifiant les ressources peu utilisées. Activer Bonjour portail Azure :

![Capture d’écran du bouton Azure Advisor dans le portail Azure](./media/billing-getting-started/advisor-button.PNG)

Ensuite, vous pouvez obtenir des conseils Bonjour **coût** onglet dans le tableau de bord hello Advisor :

![Exemple de recommandation en matière de coûts d’Advisor](./media/billing-getting-started/advisor-action.PNG)

Pour plus d’informations, consultez [Recommandations du conseiller en matière de coût](../advisor/advisor-cost-recommendations.md).

### <a name="billing-api"></a>API de facturation

Utilisez notre facturation API tooprogrammatically obtenir l’utilisation des données. Utilisez hello RateCard API et hello tooget ensemble d’API d’utilisation de l’utilisation de la facturation. Pour plus d’informations, consultez [Obtenir une vue d’ensemble de votre consommation des ressources Microsoft Azure](billing-usage-rate-card-overview.md).

## <a name="other-offers"></a> Ressources supplémentaires te cas spéciaux

### <a name="ea-csp-and-sponsorship-customers"></a>Clients EA, CSP et Sponsoring
Contactez le responsable de compte tooyour ou tooget partenaire Azure a démarré.

| Offer | les ressources |
|-------------------------------|-----------------------------------------------------------------------------------|
| Contrat Entreprise (EA) | [Portail EA](https://ea.azure.com/), [documents d’aide](https://ea.azure.com/helpdocs), et [Rapport Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-enterprise/) |
| Fournisseur de solutions cloud (CSP) | Contactez le fournisseur de tooyour |
| Azure Sponsorship | [Portail Sponsorship](https://www.microsoftazuresponsorships.com/) |

Si vous gérez des informatique pour une grande entreprise, nous vous recommandons la lecture [une vue de structure Azure enterprise](../azure-resource-manager/resource-manager-subscription-governance.md) et hello [entreprise livre blanc IT](http://download.microsoft.com/download/F/F/F/FFF60E6C-DBA1-4214-BEFD-3130C340B138/Azure_Onboarding_Guide_for_IT_Organizations_EN_US.pdf) (téléchargement .pdf, en anglais uniquement).

### <a name="check-your-subscription-and-access"></a>Vérifiez votre abonnement et votre accès

Exiger des coûts d’affichage [informations de toobilling d’accès au niveau des abonnements](billing-manage-access.md), mais hello seul l’administrateur de compte peut accéder aux hello [centre des comptes](https://account.windowsazure.com/Home/Index), modifier des informations de facturation et de gérer les abonnements. administrateur de compte Hello est personne hello problème s’est produit par le biais du processus d’inscription hello. Pour plus d’informations, consultez [ajouter ou modifier les rôles administrateur Azure qui gèrent les abonnement hello ou services](billing-add-change-azure-subscription-administrator.md).

toosee si vous êtes hello admin. compte, accédez à toohello [panneau abonnements Bonjour Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade) et examinez la liste hello d’avoir accès à des abonnements. Regardez sous **Mon rôle**. S’il est indiqué *Administrateur de compte*, vous disposez bien de tous les droits associés. S’il est indiqué autre chose, par exemple *Propriétaire*, vous ne disposez pas de privilèges complets.

![Affichage des abonnements de capture d’écran de votre rôle Bonjour Bonjour portail Azure](./media/billing-getting-started/sub-blade-view.PNG)

Si vous n’êtes pas hello admin. compte, une personne probablement vous a donné accès partiel via [contrôle d’accès basé sur le rôle d’Active Directory Azure](../active-directory/role-based-access-control-configure.md) (RBAC). toomanage abonnements et modifier vos informations, de facturation [trouver admin. compte hello](billing-subscription-transfer.md#whoisaa) et demandez-lui de tâches de hello tooperform ou [transfert hello abonnement tooyou](billing-subscription-transfer.md).

Si votre administrateur de compte n’est plus dans votre organisation et que vous devez toomanage facturation, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). 
## <a name="need-help-contact-support"></a>Vous avez besoin d’aide ? Contacter le support technique

Si vous avez besoin d’aide, [contactez le support technique](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) tooget votre problème résolu rapidement.
