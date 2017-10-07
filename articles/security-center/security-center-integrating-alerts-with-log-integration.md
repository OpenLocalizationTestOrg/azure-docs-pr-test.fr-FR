---
title: "alertes du centre de sécurité Azure aaaIntegrating avec Azure journal intégration | Documents Microsoft"
description: "Cet article vous aidera à vous familiariser avec l’intégration des alertes du Centre de sécurité avec les journaux Azure."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: d2d088d3-d38d-47ff-a062-c78e0fd59226
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: terrylan
ms.openlocfilehash: 2649036ee990bf0f48fa0cb35c7495ac932c29ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-security-center-alerts-with-azure-log-integration"></a>Intégration des alertes de l’Azure Security Center avec les journaux Azure
De nombreuses opérations de sécurité et les équipes de réponse aux incidents s’appuient sur une solution d’informations sur la sécurité et de gestion des événements (SIEM) en tant que point de départ pour le triage et examen des alertes de sécurité de hello. Avec l’intégration des journaux Azure, vous pouvez intégrer les alertes d’Azure Security Center à votre solution SIEM.

L’intégration des journaux Azure prend actuellement en charge HP ArcSight, Splunk et IBM QRadar.

## <a name="what-logs-can-i-integrate"></a>Quels journaux puis-je intégrer ?
Azure génère une journalisation complète pour chaque service. Ces journaux sont classés de la façon suivante :

* **Des journaux de contrôle/gestion** qui offrent une visibilité en hello les opérations de création de gestionnaire de ressources Azure, UPDATE et DELETE. Ces événements de plan de contrôle sont signalées Bonjour Azure journaux d’activité
* **Journaux de données de plan** qui offrent une visibilité en hello déclenchés lors de l’utilisation d’une ressource Azure. Un exemple est le journal des événements Windows hello, où vous pouvez obtenir des informations sur les événements de sécurité de canal de sécurité de l’Observateur d’événements hello. Les événements de plan de données (qui sont générés par une machine virtuelle ou un service Azure) sont signalés par les journaux de diagnostic Azure.

Intégration des journaux Azure prend actuellement en charge l’intégration de hello :

* Journaux des machines virtuelles Azure
* Journaux d’audit Azure
* Alertes Azure Security Center

## <a name="install-azure-log-integration"></a>Installer l’intégration des journaux Azure
Téléchargez [Intégration des journaux Azure](https://www.microsoft.com/download/details.aspx?id=53324).

Hello service d’intégration Azure log collecte les données de télémétrie d’ordinateur hello sur lequel il est installé.  Les données de télémétrie recueillies sont les suivantes :

* Les exceptions qui se produisent pendant l’exécution de l’intégration des journaux Azure
* Métriques sur le nombre de hello de requêtes et des événements traités
* Des statistiques sur les options de ligne de commande Azlog.exe utilisées

> [!NOTE]
> Vous pouvez désactiver la collecte des données de télémétrie en décochant cette option.
>
>

## <a name="integrate-azure-audit-logs-and-security-center-alerts"></a>Intégrer les alertes des journaux d’audit Azure et de Security Center
1. Invite de commandes ouverte hello et **cd** dans **c:\Program Files\Microsoft Azure journal intégration**.
2. Exécutez hello **azlog createazureid** commande toocreate une [Principal de Service Azure Active Directory](../active-directory/active-directory-application-objects.md) Bonjour Azure Active Directory (AD), les clients qui hébergent hello abonnements Azure.

    Vous êtes invité à entrer vos identifiants de connexion Azure.

   > [!NOTE]
   > Vous devez être l’abonnement hello propriétaire ou un Coadministrateur de l’abonnement de hello.
   >
   >

    TooAzure de l’authentification est effectuée via Azure AD.  Création d’un principal de service pour l’intégration d’Azure log crée hello Azure AD identity donné accès tooread à partir d’abonnements Azure.
3. Exécutez hello **azlog autoriser <SubscriptionID>**  tooassign accès en lecture sur hello abonnement toohello principal du service créé à l’étape 2 de la commande. Si vous ne spécifiez pas un **SubscriptionID**, puis de principal du service hello est attribué hello lecteur rôle tooall abonnements toowhich vous avez accès.

   > [!NOTE]
   > Avertissements peuvent s’afficher si vous exécutez hello **autoriser** commande immédiatement après hello **createazureid** commande. Il existe une latence entre la création de compte de hello Azure AD et quand le compte de hello est disponible pour utilisation. Si vous attendez environ 10 secondes après l’exécution de hello **createazureid** commande toorun hello **autoriser** de commandes, puis vous ne devez pas voir ces avertissements.
   >
   >
4. Vérifier hello suivant tooconfirm de dossiers qui hello les journaux d’Audit JSON :

   * **c:\Users\azlog\AzureResourceManagerJson**
   * **c:\Users\azlog\AzureResourceManagerJsonLD**
5. Vérifiez hello suivant tooconfirm dossiers figurant dans les alertes du centre de sécurité :

   * **c:\Users\azlog\ AzureSecurityCenterJson**
   * **c:\Users\azlog\AzureSecurityCenterJsonLD**
6. Configurer hello SIEM fichier redirecteur connecteur toohello dossier approprié. procédure de Hello dépend hello SIEM que vous utilisez.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur les journaux d’activité Azure et les définitions de propriétés, consultez :

* [Opérations d’audit avec Resource Manager](../azure-resource-manager/resource-group-audit.md)

toolearn en savoir plus sur le centre de sécurité, voir hello :

* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) : en savoir comment les alertes toosecurity toomanage et y répondre.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche.
* [Blog de sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : obtenir les dernières informations de sécurité Azure hello et informations.
