---
title: Forum aux questions pour Azure Cost Management | Microsoft Docs
description: "Fournit des réponses à certaines des questions les plus fréquemment posées sur Azure Cost Management."
services: cost-management
keywords: 
author: bandersmsft
ms.author: banders
ms.date: 12/14/2017
ms.topic: article
ms.service: cost-management
manager: carmonm
ms.custom: 
ms.openlocfilehash: f62e5a224c2fb33714a80bc47b98238208b787e5
ms.sourcegitcommit: 357afe80eae48e14dffdd51224c863c898303449
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/15/2017
---
# <a name="frequently-asked-questions-for-azure-cost-management"></a>Forum aux questions pour Azure Cost Management

Cet article traite des questions courantes sur Azure Cost Management (également appelé Cloudyn). Si vous avez des questions sur la Gestion des coûts, vous pouvez les poser dans le forum  [FAQs for Azure Cost Management by Cloudyn](https://social.msdn.microsoft.com/Forums/en-US/231bf072-2c71-4121-8339-ac9d868137b9/faqs-for-azure-cost-management-by-cloudyn?forum=Cloudyn).

## <a name="how-can-i-resolve-common-indirect-enterprise-setup-problems"></a>Comment puis-je résoudre des problèmes courants de configuration d’entreprise indirecte ?

Lorsque vous utilisez le portail Cloudyn pour la première fois, les messages suivants peuvent s’afficher si vous disposez d’un contrat Entreprise ou de fournisseur de solutions cloud (CSP) :

- « La clé d’API spécifiée n’est pas une clé d’inscription de niveau supérieur », dans l’Assistant **Configurer Azure Cost Management**.
- « Inscription directe – Non », sur le portail Contrat Entreprise.
- « Aucune donnée d’utilisation trouvée pour les 30 derniers jours. Contactez votre distributeur pour vous assurer que le balisage a été activé pour votre compte Azure », sur le portail Cloudyn.

Ces messages indiquent que vous avez acheté un Contrat Entreprise Azure via un revendeur ou un CSP. Votre revendeur ou CSP doit activer le _balisage_ pour votre compte Azure afin que vous puissiez afficher vos données dans Cloudyn.

Voici comment corriger les problèmes :

1. Votre revendeur doit activer le _balisage_ pour votre compte. Consultez les instructions sous [Indirect Customer Onboarding Guide](https://ea.azure.com/api/v3Help/v2IndirectCustomerOnboardingGuide) (Guide d’intégration de client indirecte).

2. Vous générez la clé Azure Enterprise Agreement à utiliser avec Cloudyn. Consultez les instructions sous [Adding Your Azure EA](https://support.cloudyn.com/hc/en-us/articles/210429585-Adding-Your-AZURE-EA) (Ajout de votre Azure EA) ou [How to Find Your EA Enrollment ID and API Key](https://youtu.be/u_phLs_udig) (Comment trouver l’ID d’inscription EA et la clé API).

Seul un administrateur de service Azure peut activer la Gestion des coûts. Les autorisations de coadministrateur sont insuffisantes.

Afin de pouvoir générer la clé API Azure Enterprise Agreement pour configurer Cloudyn, activez l’API de facturation Azure en suivant les instructions sous :

- [Vue d’ensemble des API de création de rapports pour les clients Enterprise](../billing/billing-enterprise-api.md)
- [API de création de rapports Microsoft Azure Enterprise Portal](https://ea.azure.com/helpdocs/reportingAPI) sous **Autoriser l’API à accéder aux données**


Vous devrez peut-être également accorder aux administrateurs de service, propriétaires de compte et administrateurs d’entreprise l’autorisation _d’afficher les frais_ avec l’API de facturation.

## <a name="why-dont-i-see-optimizer-recommendations"></a>Pourquoi je ne vois pas les recommandations de l’optimiseur ?

Les informations de recommandation ne sont disponibles que pour les comptes activés. Vous ne verrez pas d’informations de recommandation dans les catégories de rapport de l’**optimiseur** pour les comptes qui sont *désactivés*, y compris :

- Gestionnaire d’optimisation
- Optimisation des prix
- Manque d’efficacité

Si vous ne pouvez pas afficher les données de recommandation de l’optimiseur, vous avez probablement des comptes qui sont désactivés. Pour activer un compte, vous devez l’inscrire avec vos informations d’identification Azure.

Pour activer un compte :

1.  Dans le portail Cloudyn, cliquez sur **Settings (Paramètres)** dans le coin supérieur droit et sélectionnez **Cloud Accounts (comptes cloud)**.
2.  Dans l’onglet Comptes Microsoft Azure, recherchez les comptes dont l’abonnement est **désactivé**.
3.  À la droite d’un compte désactivé, cliquez sur le symbole **Modifier** qui ressemble à un crayon.
4.  Vos ID client et ID taux sont détectés automatiquement. Cliquez sur **Suivant**.
5.  Vous êtes redirigé vers le portail Azure. Connectez-vous au portail et autorisez le collecteur Cloudyn à accéder à vos données Azure.
6.  Ensuite, vous êtes redirigé vers la page de gestion des comptes Cloudyn et votre abonnement est mis à jour avec un état du compte **actif**. Il affiche un symbole de coche verte.
7.  Si vous ne voyez pas un symbole de coche verte pour un ou plusieurs des abonnements, cela signifie que vous n’avez pas d’autorisations pour créer une application de lecteur (le CloudynCollector) pour l’abonnement. Un utilisateur avec des autorisations plus élevées pour l’abonnement doit répéter les étapes 3 et 4.  

Après avoir effectué les étapes précédentes, vous pouvez afficher les recommandations de l’optimiseur au bout d’un ou deux jours. Toutefois, cela peut prendre jusqu’à cinq jours avant que les données complètes d’optimisation ne soient disponibles.


## <a name="how-do-i-enable-suspended-or-locked-out-users"></a>Comment faire pour activer les utilisateurs suspendus ou verrouillés ?

Si vous recevez une alerte vous demandant d’autoriser l’accès pour un utilisateur, vous devez activer le compte d’utilisateur.

Pour activer le compte d’utilisateur :

1. Connectez-vous à Cloudyn à l’aide du compte d’utilisateur administrateur Azure que vous avez utilisé pour configurer Cloudyn. Ou connectez-vous avec un compte d’utilisateur qui bénéficie de l’accès administrateur.

2. Sélectionnez le symbole d’engrenage dans le coin supérieur droit et sélectionnez **User Management** (Gestion des utilisateurs).

3. Recherchez l’utilisateur, sélectionnez l’icône du crayon, puis modifiez l’utilisateur.

4. Sous **User status** (État de l’utilisateur), modifiez l’état de **Suspended** (Suspendu) à **Active** (Actif).

Les comptes d’utilisateur Cloudyn se connectent à l’aide de l’authentification unique à partir d’Azure. Si un utilisateur ne saisit pas correctement son mot de passe, il peut être verrouillé dans Cloudyn, même s’il a toujours accès à Azure.

Si vous modifiez votre adresse e-mail dans Cloudyn pour une adresse autre que l’adresse par défaut dans Azure, votre compte risque d’être verrouillé. L’erreur suivante peut s’afficher : « status initiallySuspended. » Si votre compte d’utilisateur est verrouillé, contactez un autre administrateur pour réinitialiser votre compte.

Nous vous recommandons de créer au moins deux comptes d’administrateur Cloudyn au cas où l’un des comptes serait verrouillé.

Si vous ne pouvez pas vous connecter au portail Cloudyn, vérifiez que vous utilisez l’URL Azure Cost Management correcte pour vous connecter à Cloudyn. Utilisez [https://azure.cloudyn.com](https://ms.portal.azure.com/#blade/Microsoft_Azure_CostManagement/CloudynMainBlade).

Évitez d’utiliser l’URL Cloudyn directe https://app.cloudyn.com.

## <a name="how-do-i-activate-unactivated-accounts-with-azure-credentials"></a>Activation de comptes désactivés avec les informations d’identification Azure

Dès que vos comptes Azure sont découverts par Cloudyn, les données de coût sont immédiatement fournies dans des rapports basés sur les coûts. Toutefois, pour que Cloudyn fournisse des données sur l’utilisation et les performances, vous devez enregistrer vos informations d’identification Azure pour les comptes. Pour obtenir des instructions, consultez la page [Add Azure Resource Manager](https://support.cloudyn.com/hc/en-us/articles/212784085-Adding-Azure-Resource-Manager) (Ajouter Azure Resource Manager).

Pour ajouter des informations d’identification Azure pour un compte, dans le portail Cloudyn, sélectionnez le symbole de modification à droite du nom du compte, pas de l’abonnement.

Tant que vos informations d’identification Azure ne sont pas ajoutées dans Cloudyn, le compte apparaît comme étant _non activé_.

## <a name="how-do-i-add-multiple-accounts-and-entities-to-an-existing-subscription"></a>Comment ajouter plusieurs comptes et entités à un abonnement existant ?

Les entités supplémentaires sont utilisées pour ajouter des Contrats Entreprise supplémentaires dans un abonnement Cloudyn. Les liens suivants décrivent comment ajouter des entités supplémentaires :

- Article [Ajout d’une entité](https://support.cloudyn.com/hc/en-us/articles/212016145-Adding-an-Entity)
- Vidéo [Définition de votre hiérarchie avec les entités de coût](https://support.cloudyn.com/hc/en-us/articles/115005142529-Video-Defining-your-hierarchy-with-Cost-Entities)

Pour les CSP :

Pour ajouter des comptes CSP supplémentaires à une entité, sélectionnez **MSP Access** (Accès MSP) au lieu de **Enterprise** (Entreprise) lorsque vous créez la nouvelle entité. Si votre compte est inscrit en tant qu’Accord Entreprise et si vous souhaitez ajouter des informations d’identification CSP, le service de support technique Cloudyn devra peut-être modifier les paramètres de votre compte. Si vous êtes un abonné Azure payant, vous pouvez créer une nouvelle demande de support dans le portail Azure. Sélectionnez **Aide + Support**, puis **Nouvelle demande de support**.

## <a name="currency-symbols-in-cloudyn-reports"></a>Symboles monétaires dans les rapports Cloudyn

Vous pouvez avoir plusieurs comptes Azure utilisant des devises différentes. Toutefois, les rapports de coût dans Cloudyn n’affichent pas plus d’un type de devise par rapport.

Si vous disposez de plusieurs abonnements avec des devises différentes, une entité parente et ses devises d’entité enfant sont affichées avec le symbole **$**. La bonne pratique que nous suggérons est d’éviter d’utiliser des devises différentes dans la même hiérarchie d’entité. En d’autres termes, tous vos abonnements organisés dans une structure d’entités doivent utiliser la même devise.

Cloudyn détecte automatiquement la devise de votre abonnement Contrat Entreprise et la présente correctement dans les rapports.  En revanche, Cloudyn affiche uniquement le symbole **$** pour les comptes Azure directs web et les comptes CSP.

## <a name="what-are-cloudyn-data-refresh-timelines"></a>Que sont les chronologies d’actualisation des données de Cloudyn ?

Cloudyn dispose des chronologies d’actualisation des données suivantes :

- **Initial (Initiale)** : l’affichage des données de coût dans Cloudyn après la configuration peut prendre jusqu’à 24 heures. Cloudyn peut également nécessiter jusqu’à 10 jours afin de collecter les données nécessaires pour afficher les recommandations de dimensionnement.
- **Daily (Quotidienne)** : à partir du dixième jour jusqu’à la fin de chaque mois, Cloudyn doit afficher vos données à jour depuis la veille jusqu’à environ UTC+3 le jour suivant.
- **Monthly (Mensuelle)** : du premier jour au dixième jour de chaque mois, Cloudyn peut n’afficher vos données que jusqu’à la fin du mois précédent.

Cloudyn traite les données du jour précédent lorsque des données complètes pour le jour précédent sont disponibles. Les données du jour précédent sont généralement disponibles dans Cloudyn avec un décalage UTC+3 chaque jour. Le traitement de certaines données, telles que les balises, peut prendre 24 heures supplémentaires.

Les données du mois en cours ne sont pas disponibles pour la collecte au début de chaque mois. Durant la période, les fournisseurs de services finalisent leur facturation pour le mois précédent. Les données du mois précédent s’affichent dans Cloudyn 5 à 10 jours après le début de chaque mois. Pendant ce temps, seuls les coûts amortis du mois précédent peuvent s’afficher. Les données de facturation ou d’utilisation quotidiennes peuvent ne pas s’afficher. Lorsque les données deviennent disponibles, Cloudyn les traite de façon rétroactive. Après le traitement, toutes les données mensuelles s’affichent entre le 5 et le 10 de chaque mois.

En cas de délai d’envoi des données à partir d’Azure vers Cloudyn, les données sont toujours enregistrées dans Azure. Les données sont transférées à Cloudyn lorsque la connexion est rétablie.

## <a name="how-can-a-direct-csp-configure-cloudyn-access-for-indirect-csp-customers-or-partners"></a>Comment un CSP direct peut-il configurer l’accès à Cloudyn pour les clients ou partenaires d’un CSP indirect ?

Pour obtenir des instructions, consultez [Configurer l’accès CSP indirect dans Cloudyn](quick-register-csp.md#configure-indirect-csp-access-in-cloudyn).

## <a name="what-causes-the-optimizer-menu-item-to-appear"></a>Pourquoi l’élément de menu Optimizer (Optimiseur) apparaît-il ?

Après l’ajout de l’accès à Azure Resource Manager et la collection des données, vous devriez voir l’option **Optimizer (Optimiseur)**. Pour activer l’accès à Azure Resource Manager, consultez [Activation de comptes désactivés avec les informations d’identification Azure](#how-do-i-activate-unactivated-accounts-with-azure-credentials).

## <a name="is-cost-managementcloudyn-agent-based"></a>Cost Management/Cloudyn est-il basé sur un agent ?

Non. Les agents ne sont pas utilisés. Les données métriques de machine virtuelle Azure pour les machines virtuelles sont collectées à partir de l’API Microsoft Insights. Si vous souhaitez collecter des données métriques à partir de machines virtuelles Azure, ces dernières doivent avoir les paramètres de diagnostic activés.

## <a name="do-cloudyn-reports-show-more-than-one-ad-tenant-per-report"></a>Les rapports Cloudyn affichent-ils plusieurs locataires AD par rapport ?

Oui. Vous pouvez [créer une entité de compte cloud correspondante](tutorial-user-access.md#create-entities) pour chacun de vos locataires Active Directory. Vous pouvez ensuite afficher toutes vos données de locataire Azure AD et d’autres fournisseurs de plateforme cloud, notamment Amazon Web Services et Google Cloud Platform.
