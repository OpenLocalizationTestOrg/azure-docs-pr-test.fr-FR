---
title: "aaaComparing Azure Mobile Engagement avec d’autres services Azure similaires"
description: Comparaison entre Azure Mobile Engagement et des services Azure similaires - HockeyApp, AppInsights, Notification Hubs
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1f114775-3a9a-4dd4-8d59-b10d1da9a68b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0859ae9980d0fa96ffbc0edfbd795ccc58d2c843
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="comparing-azure-mobile-engagement-with-other-similar-azure-services"></a>Comparaison entre Azure Mobile Engagement et des services Azure similaires
liste de Hello des services proposés par Microsoft Azure est jamais développant et dans certains cas, vous pouvez vous demander comment diffère Azure Mobile Engagement cette autre service que vous venez de lire ou Découvrez. Cet article tente de risques de confusion tooclear hello et vous dirige toochoose Azure Mobile Engagement lorsqu’il est plus approprié pour votre utilisation. 

Azure Mobile Engagement est un service destiné spécifiquement **pour les spécialistes du marketing/CMOs numériques** mais peut être utilisé par les **propriétaire de l’application mobile ou le serveur de publication** qui veut tooincrease utilisation de hello, rétention et monétisation de leurs applications mobiles. 

*Azure Mobile Engagement est une plateforme SaaS d'engagement des utilisateurs qui fournit des informations orientées données sur l'utilisation des applications, qui permet de segmenter les utilisateurs en temps réel et d'activer les notifications Push adaptées au contexte, ainsi que la messagerie au sein de l'application.* 

Décomposer cette définition, nous avons hello suivante des principales caractéristiques qui met également en surbrillance la proposition de valeur unique :

1. **Notifications Push contextuelles et messagerie dans l’application**
   
   Il s’agit principalement de produit de hello hello - effectuer des notifications push ciblés et personnalisés. Et, pour cette toohappen, nous collecter des données de l’analytique comportementale riche. 
2. **Informations pilotées par les données sur l’utilisation des applications**
   
   Nous fournissons inter-plateformes kits de développement logiciel toocollect hello comportementales analytique sur les utilisateurs d’application hello. Notez l’analytique comportementale de terme hello (comme sur l’analytique des performances), car nous concentrer sur la manière dont les utilisateurs d’application hello utilisent application hello. Nous collectons données analytique de performances de base sur les erreurs, etc. de pannes, mais qui est pas hello traite principalement de produit de hello. 
3. **Segmentation des utilisateurs en temps réel**
   
   Une fois que vous avez collecté les données analytique comportementales des utilisateurs de l’application, nous permettent une toosegment votre audience en fonction des paramètres différents, tooenable les données collectées vous toorun ciblé campagnes de push. 
4. **Logiciel en tant que service (SaaS) :**
   
   Nous ont un portail distinct à partir du portail de gestion Azure hello qui est optimisé toointeract et afficher riche analytique comportementale sur les utilisateurs d’application hello et exécuter des campagnes de push. produit de Hello est adapté tooget allez-vous sans délai !   

Avec ce paramètre de différenciation dans main, voici comment nous comparer par rapport à d’autres offres Azure apparemment similaires - Notez cet article hello n’effectue une comparaison au niveau de fonctionnalité, mais prend une plus toodefine d’approche scénario basé le produit fonctionne mieux :

1. [HockeyApp](https://azure.microsoft.com/services/hockeyapp/) est hello mobile DevOps solution Microsoft. Avec lui, vous pouvez distribuer les builds toobeta testeurs, collecter des données de panne et obtenir des commentaires des utilisateurs. La solution est également intégrée avec Visual Studio Team Services, ce qui permet d’activer des déploiements de versions simples et d’intégrer des éléments de travail. 
   
   Hello est de DevOps et collecte des données analytique de performances sur les applications mobiles hello. Vous risquez avec intégration à la fois HockeyApps et Mobile Engagement dans votre application et qui ne sera pas inhabituelle, même s’il existe certains chevauchement des données de salutation collectée, principalement des produits de hello hello est différent et ils vous aident à atteindre différents objectifs pour vous.  
2. [Application Insights](../application-insights/app-insights-overview.md) si votre application mobile a une côté serveur, puis vous utilisez Application Insights toomonitor hello web côté serveur de votre application, mais pour les applications mobiles hello client côté, vous devez utiliser HockeyApp. 
3. [Concentrateurs de notification](https://azure.microsoft.com/services/notification-hubs/) fournit un service léger sens hello que vous n’avez pas besoin d’un kit de développement intégré dans l’application mobile hello et vous pouvez avoir un contrôle total de votre application mobile, et il autorise l’envoi de notifications push avec des fonctionnalités de balisage de base. C’est parfait pour n’importe quel propriétaire de l’application qui prend soin inférieur sur le ciblage et plus sur les informations d’envoi/de communiquer instantanément tootheir d’utilisateurs d’application (diffusion tooa grand remplissage). 
   
   Notez le focus hello ici lors de l’envoi des notifications rapides avec la fonctionnalité de segmentation de base. 

Examinons quelques scénarios :

1. TIM est la partie de l’équipe marketing de hello numérique dans le magasin de Adventure Works qui publie des applications mobiles pour les utilisateurs. Les objectifs de TIM sont tooensure que les utilisateurs de hello qui téléchargent leurs applications mobiles continuent toouse il et fréquemment. Cela augmente pas simplement une marque de joindre avec les utilisateurs d’application hello, mais également la monétisation augmente lorsque les utilisateurs d’application hello faire des achats à l’aide d’application mobile hello. Pour cet Tim devez toosend ciblé notifications toohello application aux utilisateurs, qui elles utiles, tooencourage les tooopen hello application et revenez tooit souvent. Mobile Engagement correspond donc parfaitement à ses attentes. 
2. JoAnn fait partie de l’équipe de développement hello Hello des applications mobiles à Adventure Works et recherche les détails sur un toolog le produit sur les blocages, les exceptions et obtenir des données de télémétrie de performances à partir d’une application. HockeyApp correspond donc parfaitement à ses attentes. JoAnn peut intégrer les deux HockeyApp pour son développeur destiné aux scénarios et Azure Mobile Engagement dans Tim Bonjour même hello tooget application meilleur des deux. 
3. (Round Robin) fait partie de l’équipe de développement hello de hello des applications mobiles au réseau de Contoso actualités et tous les souhaitées est toosend les dernières nouvelles alertes tooall les utilisateurs sans quantité segmentation hello news alerte est déclenchée dès que. Notification Hubs correspond donc parfaitement à ses attentes. 
   Dans ce scénario, il est possible cependant que comme application mobile hello arrive à maturité, il y a une exigence toodo détails beaucoup plus riches de segmentation et get sur le comportement de l’utilisateur d’application hello. À ce stade, (Round Robin) aura tooevaluate Azure Mobile Engagement. 

toorecap, hello Mobile Engagement ne vise pas simplement toocollect analytique - il n’est pas « encore un autre produit de l’Analytique de Microsoft ». Il s’agit de l’envoi de notifications push ciblé et pour le ciblage, nous collecter des données de l’analytique comportementale, mais le focus de hello reste sur l’envoi de notifications push qui hello la plupart des utilisateurs d’application de toohello sens afin qu’il n’est fourni en tant que courrier indésirable. 

Pour plus d’informations, consultez cette [courte vidéo](mobile-engagement-overview.md) sur Mobile Engagement. 

