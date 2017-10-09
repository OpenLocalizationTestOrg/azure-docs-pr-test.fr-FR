---
title: "aaaAzure intégration du journal avec le centre de sécurité | Documents Microsoft"
description: "Découvrez comment tooget Azure Security center alertes fonctionne avec l’intégration du journal"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 03/22/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: bcc208d071ec03738215f2aee3b71c7b10927904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-your-security-center-alerts-in-azure-log-integration"></a>Comment tooget votre centre de sécurité des alertes dans l’intégration d’Azure log
Cet article fournit hello étapes tooenable requis hello Azure journal Integration service toopull informations sur les alertes de sécurité générées par le centre de sécurité Azure. Vous devez avoir terminé avec succès les étapes hello Bonjour [prise en main](security-azure-log-integration-get-started.md) article avant d’effectuer les étapes de hello dans cet article.

## <a name="detailed-steps"></a>Procédure détaillée
Hello suit créera hello requis Principal de Service Azure Active Directory et d’autorisations de lecture assign hello SPN toohello abonnement :
1. Ouvrez l’invite de commandes hello et accédez trop**c:\Program Files\Microsoft Azure journal d’intégration**
2. Exécutez la commande hello``azlog createazureid``

    Cette commande vous invite à entrer votre nom d’utilisateur Azure. commande Hello crée ensuite un [Principal de Service Azure Active Directory](../active-directory/develop/active-directory-application-objects.md) Bonjour clients Azure AD qui hébergent hello abonnements Azure qui Bonjour à l’utilisateur connecté est un administrateur, un Coadministrateur ou un propriétaire. commande Hello échouera si hello à l’utilisateur connecté est un utilisateur invité Bonjour client Azure AD. TooAzure de l’authentification est effectuée via Azure Active Directory (AD). Création d’un principal de service pour l’intégration de Azlog crée hello identité Azure AD qui aura accès tooread à partir d’abonnements Azure.

2. Ensuite, vous allez exécuter une commande qui affecte l’accès en lecture sur hello abonnement toohello principal du service créé à l’étape 2. Si vous ne spécifiez pas un ID d’abonnement, commande hello tentera tooassign hello rôle service lecteur principal tooall abonnements toowhich vous avez accès. </br></br>
``azlog authorize <SubscriptionID>`` </br> par exemple </br>
``azlog authorize 0ee55555-0bc4-4a32-a4e8-c29980000000``

    >[!NOTE]
    Avertissements peuvent s’afficher si vous exécutez hello autoriser commande immédiatement après la commande de createazureid hello. Il existe une latence entre la création de compte de hello Azure AD et quand le compte de hello est disponible pour utilisation. Si vous attendez environ 60 secondes après l’exécution de commande toorun hello hello createazureid autoriser la commande, puis vous ne devez pas voir ces avertissements.

4. Vérifier hello suivant tooconfirm de dossiers qui hello les journaux d’Audit JSON :
 * **c:\Users\azlog\AzureResourceManagerJson**
 * **c:\Users\azlog\AzureResourceManagerJsonLD** </br></br>
5. Vérifiez hello suivant tooconfirm dossiers figurant dans les alertes du centre de sécurité :</br></br>
 * **c:\Users\azlog\AzureSecurityCenterJson**
 * **c:\Users\azlog\AzureSecurityCenterJsonLD** </br></br>

Si vous rencontrez des problèmes pendant l’installation de hello et de configuration, ouvrez un [demande de support](/azure-supportability/how-to-create-azure-support-request.md), sélectionnez **journal intégration** en tant que service hello pour lequel vous demandez la prise en charge.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur l’intégration des journaux Azure, consultez hello suivant des documents :

* [Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) : Centre de téléchargement pour plus d’informations, la configuration système requise et les instructions d’installation sur l’intégration des journaux Azure.
* [Intégration du journal tooAzure introduction](security-azure-log-integration-overview.md) : ce document présente tooAzure journal intégration, ses fonctionnalités clées, et comment il fonctionne.
* [Étapes de configuration du partenaire](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – ce billet de blog montre comment tooconfigure Azure du journal toowork d’intégration avec les solutions de partenaire Splunk, HP ArcSight et QRadar d’IBM.
* [FAQ de l’intégration des journaux Azure](security-azure-log-integration-faq.md) : ce forum aux questions répond aux questions sur l’intégration des journaux Azure.
* [Intégration de centre de sécurité les alertes avec Azure journal intégration](../security-center/security-center-integrating-alerts-with-log-integration.md) – ce document vous montre comment le centre de sécurité toosync des alertes, ainsi que des événements de sécurité d’ordinateur virtuel collectées par Diagnostics Azure et les journaux d’Audit Azure, avec votre analytique de journal ou Solution SIEM.
* [Nouvelles fonctionnalités pour les diagnostics Azure et les journaux d’Audit Azure](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) – ce billet de blog vous présente les journaux d’Audit de tooAzure et autres fonctionnalités qui vous aident à obtenir les opérations hello de vos ressources Azure.
