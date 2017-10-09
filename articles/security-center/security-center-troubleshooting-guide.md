---
title: "Guide de résolution des problèmes de centre de sécurité d’aaaAzure | Documents Microsoft"
description: "Ce document vous aide à tootroubleshoot des problèmes dans le centre de sécurité Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 44462de6-2cc5-4672-b1d3-dbb4749a28cd
ms.service: security-center
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/11/2017
ms.author: yurid
ms.openlocfilehash: 78b3c49eb66fe3a4f80efbba3a47a87b039c07ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-troubleshooting-guide"></a>Guide de résolution des problèmes d’Azure Security Center
Ce guide est pour les professionnels de l’informatique, aux analystes en sécurité des informations et des administrateurs de cloud dont organisations utilisent Azure Security Center et nécessitent le que centre de sécurité tootroubleshoot les problèmes liés.

>[!NOTE] 
>À compter de début juin 2017, centre de sécurité utilise des données de toocollect et le magasin de Microsoft Monitoring Agent de hello. Consultez [Migration de plateforme Azure Security Center](security-center-platform-migration.md) toolearn plus. informations Hello dans cet article représentent les fonctionnalités du centre de sécurité après la transition toohello Microsoft Monitoring Agent.
>

## <a name="troubleshooting-guide"></a>Guide de résolution des problèmes
Ce guide explique comment les problèmes liés tootroubleshoot le centre de sécurité. La plupart des hello dépannage effectué dans le centre de sécurité a lieu en examinant en premier hello [journal d’Audit](https://azure.microsoft.com/updates/audit-logs-in-azure-preview-portal/) enregistrements pour hello Échec de composant. Les journaux d’audit vous permettent de déterminer :

* Les opérations ayant eu lieu.
* Qui a lancé une opération hello
* Lorsque l’opération de hello s’est produite
* état Hello d’opération de hello
* les valeurs Hello d’autres propriétés qui peuvent vous aider à effectuer des recherches sur les opération hello

journal d’audit de Hello contient toutes les opérations d’écriture (PUT, POST, DELETE) effectuées sur vos ressources, mais elle n’inclut pas les opérations de lecture (GET).

## <a name="microsoft-monitoring-agent"></a>Microsoft Monitoring Agent
Centre de sécurité utilise hello Microsoft Monitoring Agent – il s’agit d’hello même agent utilisé par hello Operations Management Suite et service Analytique de journal – toocollect les données de sécurité à partir de vos machines virtuelles Azure. Une fois la collecte de données est activée et hello agent est correctement installé sur l’ordinateur cible hello, processus hello ci-dessous doivent être dans l’exécution :

* HealthService.exe

Si vous ouvrez la console de gestion des services (services.msc) hello, vous verrez également en cours d’exécution service Microsoft Monitoring Agent hello comme indiqué ci-dessous :

![Services](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig5.png)

toosee version de l’agent de hello que vous avez, ouvrez **le Gestionnaire des tâches**, Bonjour **processus** onglet Rechercher hello **Service Microsoft Monitoring Agent**, avec le bouton droit sur celui-ci et Cliquez sur **propriétés**. Bonjour **détails** onglet, recherchez la version du fichier hello comme indiqué ci-dessous :

![Fichier](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig6.png)
   

## <a name="microsoft-monitoring-agent-installation-scenarios"></a>Scénarios d’installation de Microsoft Monitoring Agent
Il existe deux scénarios d’installation qui peuvent produire des résultats différents lors de l’installation hello Microsoft Monitoring Agent sur votre ordinateur. scénarios de Hello pris en charge sont :

* **L’agent installé automatiquement par le centre de sécurité**: dans ce scénario, vous serez tooview en mesure des alertes de hello dans les emplacements, le centre de sécurité et recherche de journal. Vous recevez une adresse de messagerie électronique notifications toohello qui a été configuré dans la stratégie de sécurité hello pour hello abonnement hello ressource appartient.
.
* **L’agent installé manuellement sur un ordinateur virtuel se trouve dans Azure**: dans ce scénario, si vous utilisez des agents téléchargés et installés manuellement préalable tooFebruary 2017, vous serez en mesure de tooview les alertes de hello dans le portail du centre de sécurité hello uniquement si vous filtrez sur hello espace de travail hello abonnement appartient. Dans les cas, vous filtrez sur la ressource de hello hello abonnement appartient, vous ne serez pas toosee en mesure de toutes les alertes. Vous recevrez par courrier électronique toohello adresse e-mail des notifications qui a été configuré dans la stratégie de sécurité hello pour l’espace de travail hello hello abonnement appartient.

>[!NOTE]
> comportement de hello tooavoid expliqué dans hello en second lieu, assurez-vous que vous téléchargez la version la plus récente de l’agent de hello hello.
> 

## <a name="troubleshooting-monitoring-agent-network-requirements"></a>Résolution des problèmes de configuration réseau requise de l’agent de surveillance
Pour les agents tooconnect tooand Registre avec le centre de sécurité, ils doivent avoir accès toonetwork ressources, notamment les numéros de port hello et les URL de domaine.

- Pour les serveurs proxy, vous devez tooensure qui hello du serveur proxy approprié ressources sont configurés dans les paramètres de l’agent. Lisez cet article pour plus d’informations sur [comment toochange hello les paramètres du proxy](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-windows-agents#configure-proxy-settings).
- Pour les pare-feu qui limitent l’accès toohello Internet, vous devez tooconfigure votre tooOMS d’accès de toopermit pare-feu. Aucune action n’est nécessaire dans les paramètres de l’agent.

Hello tableau suivant montre les ressources nécessaires pour la communication.

| Ressource de l'agent | Ports | Ignorer l’inspection HTTPS |
|---|---|---|
| *.ods.opinsights.azure.com | 443 | Oui |
| *.oms.opinsights.azure.com | 443 | Oui |
| *.blob.core.windows.net | 443 | Oui |
| *.azure-automation.net | 443 | Oui |

Si vous rencontrez des problèmes de l’intégration avec l’agent de hello, assurez-vous qu’article de hello tooread [comment l’intégration de Microsoft Operations Management Suite tootroubleshoot problèmes](https://support.microsoft.com/en-us/help/3126513/how-to-troubleshoot-operations-management-suite-onboarding-issues).


## <a name="troubleshooting-endpoint-protection-not-working-properly"></a>Dépannage d’une protection du point de terminaison qui ne fonctionne pas correctement

l’agent invité de Hello consiste hello parent de tous les éléments hello [Microsoft Antimalware](../security/azure-security-antimalware.md) est de l’extension. En cas d’échec du processus de l’agent invité hello, hello Microsoft Antimalware qui s’exécute comme un processus enfant de l’agent invité de hello peut également échouer.  Dans les scénarios comme qui est recommandée tooverify hello les options suivantes :

- Si la cible de hello VM est une image personnalisée et créateur hello Hello VM jamais installé l’agent invité.
- Si la cible de hello est un VM Linux au lieu d’une machine virtuelle de Windows version de Windows hello d’extension du logiciel anti-programme malveillant hello puis l’installation sur un VM Linux échoue. l’agent invité Linux de Hello a des exigences spécifiques en termes de version du système d’exploitation et les packages requis, et si ces conditions ne sont pas remplies agent de machine virtuelle hello ne fonctionnera pas il soit. 
- Si hello machine virtuelle a été créé avec une ancienne version de l’agent invité. S’il s’agissait, sachez que certains agents ancien n'impossible pas automatiquement mise à jour lui-même version plus récente de toohello, et pourrait conduire toothis problème. Utilisez toujours la version la plus récente de l’agent invité hello si la création de vos propres images.
- Certains logiciels d’administration tiers peuvent désactiver l’agent invité de hello ou bloquer l’accès aux emplacements des fichiers toocertain. Si vous avez installé sur votre machine virtuelle à des tiers, assurez-vous que l’agent hello est sur la liste d’exclusion hello.
- Certains paramètres de pare-feu ou d’un groupe de sécurité réseau (NSG) peut se bloquer tooand du trafic réseau à partir de l’agent invité.
- Certaines listes de contrôle d’accès (ACL) peuvent empêcher l’accès au disque.
- Manque d’espace disque peut bloquer l’agent invité de hello de fonctionner correctement. 

Par hello par défaut Interface utilisateur de Microsoft Antimalware est désactivé, en lecture [l’activation de Interface utilisateur contre les logiciels malveillants Microsoft sur Azure Resource Manager machines virtuelles après le déploiement](https://blogs.msdn.microsoft.com/azuresecurity/2016/03/09/enabling-microsoft-antimalware-user-interface-post-deployment/) pour plus d’informations sur la façon de tooenable si vous avez besoin.

## <a name="troubleshooting-problems-loading-hello-dashboard"></a>Dépannage des problèmes de chargement du tableau de bord hello

Si vous rencontrez des problèmes lors du chargement du tableau de bord de centre de sécurité hello, assurez-vous que l’utilisateur hello inscrit hello abonnement tooSecurity Center (c'est-à-dire hello premier utilisateur qui a ouvert le centre de sécurité avec un abonnement de hello) et l’utilisateur hello qui souhaiteraient tooturn sur collecte de données doit être *propriétaire* ou *collaborateur* lors de l’abonnement de hello. À partir de ce moment également les utilisateurs avec *lecteur* hello abonnement voyez hello du tableau de bord alertes/recommandation/stratégie /.

## <a name="contacting-microsoft-support"></a>Contacter le support Microsoft
Certains problèmes peuvent être identifiés à l’aide des instructions de hello fournies dans cet article, d’autres vous trouverez également documentées hello centre de sécurité public [Forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureSecurityCenter). Toutefois, si vous avez encore besoin d’aide pour résoudre votre problème, vous pouvez ouvrir une nouvelle demande de support à l’aide du **portail Azure**, comme indiqué ci-dessous : 

![Support Microsoft](./media/security-center-troubleshooting-guide/security-center-troubleshooting-guide-fig2.png)


## <a name="see-also"></a>Voir aussi
Dans ce document, vous avez appris comment tooconfigure des stratégies de sécurité dans le centre de sécurité Azure. toolearn en savoir plus sur Azure Security Center, voir hello :

* [Azure Security Center Guide de planification et opérations](security-center-planning-and-operations-guide.md) — Découvrez comment tooplan et comprendre les considérations de conception hello tooadopt Azure Security Center.
* [Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) — Découvrez comment toomonitor hello d’intégrité de vos ressources Azure
* [Toosecurity répond et de la gestion des alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) : en savoir comment les alertes toosecurity toomanage et y répondre
* [Surveillance des solutions de partenaire avec Azure Security Center](security-center-partner-solutions.md) — Découvrez comment toomonitor hello état d’intégrité de vos solutions de partenaire.
* [Forum aux questions sur Azure Security Center](security-center-faq.md) : Forum aux questions sur l’utilisation hello service de recherche
* [Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.

