---
title: Pratiques aaaBest pour Azure App Service
description: "Découvrez les meilleures pratiques et la résolution des problèmes pour Azure App Service."
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: f3359464-fa44-4f4a-9ea6-7821060e8d0d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/30/2016
ms.author: dariagrigoriu
ms.openlocfilehash: a1d3127f5a746aa43f7b56b45f17c45df9087bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-azure-app-service"></a>Meilleures pratiques pour Azure App Service
Cet article résume les meilleures pratiques dans l’utilisation de [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). 

## <a name="colocation"></a>Colocalisation
Lorsque la composition d’une solution telle qu’une application web et une base de données de ressources Azure sont situés dans des effets des régions différentes hello peuvent suivants hello :

* Une latence plus élevée dans la communication entre les ressources
* Transfert de frais monétaires pour les données sortantes entre régions comme indiqué sur hello [Azure page de tarification](https://azure.microsoft.com/pricing/details/data-transfers).

La colocalisation Bonjour même région est idéal pour les ressources Azure de composer une solution telle qu’une application web et un compte de base de données ou de stockage utilisé toohold contenu ou données. Lorsque la création de ressources vous devez vous assurer qu’ils sont dans hello même région Azure sauf si vous avez professionnels spécifiques ou raison toobe pas de conception. Vous pouvez déplacer une toohello d’application de Service de l’application même région que votre base de données en tirant parti de hello [fonctionnalité de clonage du Service d’applications](app-service-web-app-cloning-portal.md) actuellement disponibles pour les applications de Premium du Plan App Service.   

## <a name="memoryresources"></a>Quand les applications consomment plus de mémoire que prévu
Lorsque vous remarquez une application consomme davantage de mémoire que prévu comme indiqué par le biais d’analyse ou de recommandations de service envisagez hello [App Service la réparation automatique de fonctionnalité](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites). Une des options de hello pour la fonctionnalité de la réparation automatique hello effectue les actions personnalisées en fonction d’un seuil de mémoire. Actions span spectre hello de tooinvestigation des notifications par courrier électronique via l’atténuation de tooon place de vidage de mémoire par le recyclage des processus de travail hello. La réparation automatique peut être configurée via le fichier web.config et via une interface utilisateur conviviale conformément à ce billet de blog pour hello [Extension d’application Service prise en charge de Site](https://azure.microsoft.com/blog/additional-updates-to-support-site-extension-for-azure-app-service-web-apps).   

## <a name="CPUresources"></a>Quand les applications consomment plus d’UC que prévu
Lorsque vous remarquez qu'une application consomme plus d’UC que prévu ou rencontre de répéter les pics de consommation UC comme indiqué par le biais d’analyse ou prendre en compte des recommandations de service l’évolution verticale ou la montée en puissance parallèle hello plan App Service. Si votre application est avec état, l’évolution verticale est l’option de hello, tandis que si votre application est sans état, de mise à l’échelle de la sortie vous donne plus de souplesse et plus susceptible de mise à l’échelle. 

Pour plus d’informations sur les applications « sans état » et « avec état », visualisez la vidéo [Planning a Scalable End-to-End Multi-Tier Application on Microsoft Azure Web App](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2014/DEV-B414#fbid=?hashlink=fbid)(Planification d’une application multiniveau complète et évolutive sur l’application web Microsoft Azure). Pour plus d’informations sur les options de montée en charge et de mise à l’échelle automatique, consultez [Mise à l’échelle d’une application web dans Microsoft Azure App Service](web-sites-scale.md).  

## <a name="socketresources"></a>Quand les ressources de socket sont épuisées
Une raison courante d’épuiser les connexions TCP sortantes est hello utilisation des bibliothèques clientes qui ne sont pas les connexions TCP tooreuse implémenté, ou dans les cas de hello d’un protocole de niveau supérieur tels que HTTP - n’étant ne pas exploité Keep-Alive. Consultez la documentation de hello pour chacune des bibliothèques hello référencés par les applications hello dans votre tooensure Plan App Service qu’ils sont configurés ou accessible dans votre code pour une réutilisation efficace de connexions sortantes. Suivez également hello bibliothèque documentation des conseils pour la création correcte et mise en production ou nettoyage tooavoid une fuite de connexions. Alors que ces enquêtes de bibliothèques de client sont en impact de progression peut être atténuée par montée en puissance parallèle toomultiple instances.  

## <a name="appbackup"></a>La sauvegarde de votre application échoue
Hello deux raisons les plus courantes pour lesquelles Échec de la sauvegarde application est : les paramètres de stockage non valide et la configuration de la base de données non valide. Ces défaillances se produisent généralement lors des modifications toostorage ou des ressources de base de données ou les modifications sur la manière de tooaccess ces ressources (par exemple, informations d’identification mises à jour pour hello de base de données sélectionnée dans les paramètres de sauvegarde hello). Généralement, les sauvegardes s’exécutent selon une planification et requièrent toostorage d’accès (pour la sortie de hello des fichiers sauvegardé) et les bases de données (pour la copie et la lecture toobe contenu inclus dans la sauvegarde de hello). Hello échec tooaccess une de ces ressources serait de l’échec des sauvegardes cohérente. 

Lorsque les échecs de sauvegarde se produisent, passez en revue le plus récent toounderstand résultats quel type de défaillance se produit. Dans les cas de hello d’échecs d’accès de stockage, vérifiez et mettez à jour les paramètres de stockage hello utilisés dans la configuration de la sauvegarde hello. Dans les cas de hello d’échecs d’accès de base de données, examiner et mettre à jour vos chaînes de connexion dans le cadre des paramètres de l’application ; Passez tooupdate tooproperly de votre configuration de la sauvegarde incluent des bases de données de hello requis. Pour plus d’informations sur la sauvegarde de l’application hello consultez [sauvegardez une application web dans Azure App Service](web-sites-backup.md) documentation.

## <a name="nodejs"></a>Lorsque de nouvelles applications Node.js sont déployé tooAzure du Service d’applications
Azure App Service est par défaut pour les applications Node.js toobest prévue couleur hello besoins d’applications courantes. Si la configuration pour votre application Node.js serait tirent parti des performances tooimprove paramétrage personnalisé ou optimiser l’utilisation des ressources pour les ressources de processeur/mémoire/réseau, vous pourriez consulter nos meilleures pratiques et les étapes de dépannage. Cet article de la documentation décrit les paramètres d’iisnode hello vous devrez peut-être tooconfigure pour votre application Node.js, décrit hello de divers scénarios ou problèmes que votre application peut rencontrer et montre comment tooaddress ces problèmes : [meilleures pratiques et guide de dépannage pour les applications du nœud sur Azure App Service](app-service-web-nodejs-best-practices-and-troubleshoot-guide.md).   

