---
title: "aaaAzure journal d’intégration avec les journaux d’audit Azure Active Directory | Documents Microsoft"
description: "Découvrez comment tooinstall hello service d’intégration des journaux Azure et intégrer des journaux à partir des journaux d’audit Azure"
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
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a>Intégrer des journaux d’audit Azure Active Directory

Les événements d’audit Azure Active Directory (Azure AD) vous aident à identifier les actions privilégiées survenues dans Azure Active Directory. Vous pouvez voir hello des types d’événements que vous pouvez suivre en examinant [événements de rapport d’audit Azure Active Directory](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).

> [!NOTE]
> Avant de commencer les étapes hello dans cet article, vous devez passer en revue hello [prise en main](security-azure-log-integration-get-started.md) l’article et il les étapes hello.

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a>Azure Active directory de toointegrate suit les journaux d’audit

1. Ouvrez l’invite de commandes hello et exécutez la commande suivante :

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. Exécutez cette commande : 
 
   ``azlog createazureid``

   Cette commande vous invite à entrer votre nom d’utilisateur Azure. Hello commande crée ensuite un répertoire Azure Active Directory principal du service dans les clients hello Azure AD qui hébergent hello abonnements Azure dans le hello utilisateur connecté est un administrateur, un coadministrateur ou un propriétaire. commande Hello échoue si l’utilisateur connecté hello est uniquement un utilisateur invité dans le locataire Azure AD de hello. TooAzure de l’authentification est effectuée via Azure AD. Création d’un principal de service pour l’intégration des journaux Azure crée hello identité Azure AD donné accès tooread à partir d’abonnements Azure.

3. Exécutez hello suivant commande tooprovide votre ID de client. Vous devez toobe des membres de la commande de hello client admin rôle toorun hello.

   ``Azlog.exe authorizedirectoryreader tenantId``

   Exemple :

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. Vérifiez que hello suivant tooconfirm de dossiers qui hello Azure Active Directory JSON les journaux d’audit est créé dans les :

   * **C:\Users\azlog\AzureActiveDirectoryJson**
   * **C:\Users\azlog\AzureActiveDirectoryJsonLD**

Hello vidéo suivante montre les étapes hello abordées dans cet article :

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> Pour obtenir des instructions spécifiques à ajouter des informations de hello dans les fichiers au format JSON hello dans vos informations de sécurité et le système de gestion (SIEM) des événements, contactez votre fournisseur SIEM.

Aide de la Communauté est disponible via hello [Forum MSDN de Azure journal intégration](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Ce forum permettant dans hello Azure journal intégration communautaire toosupport eux avec des questions, des réponses, des conseils et astuces. En outre, l’équipe d’intégration du journal Azure hello surveille ce forum et permet la mesure du possible.

Vous pouvez également ouvrir une [demande de support](../azure-supportability/how-to-create-azure-support-request.md). Sélectionnez **journal intégration** en tant que service hello pour lequel vous demandez la prise en charge.

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur l’intégration des journaux Azure, consultez :

* [Microsoft Azure Log Integration](https://www.microsoft.com/download/details.aspx?id=53324) : cette page du Centre de téléchargement donne plus d’informations, la configuration système requise et les instructions d’installation pour l’intégration des journaux Azure.
* [Introduction tooAzure intégration du journal](security-azure-log-integration-overview.md): cet article vous présente tooAzure intégration du journal, ses fonctionnalités clées et comment il fonctionne.
* [Étapes de configuration du partenaire](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): ce billet de blog montre comment toowork d’intégration du journal Azure tooconfigure avec partenaire solutions Splunk, HP ArcSight et QRadar d’IBM.
* [Forum aux questions sur l’intégration des journaux Azure](security-azure-log-integration-faq.md) : cet article répond à des questions sur l’intégration des journaux Azure.
* [Intégration des alertes du centre de sécurité avec l’intégration de Azure journal](../security-center/security-center-integrating-alerts-with-log-integration.md): cet article vous explique comment le centre de sécurité toosync des alertes, ainsi que des événements de sécurité d’ordinateur virtuel collectées par Diagnostics Windows Azure et les journaux d’audit Azure, avec votre analytique de journal ou Solution SIEM.
* [Nouvelles fonctionnalités pour les Diagnostics Azure et Azure des journaux d’audit](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): ce billet de blog vous présente les journaux d’audit tooAzure et autres fonctionnalités qui vous aident à obtenir les opérations hello de vos ressources Azure.
