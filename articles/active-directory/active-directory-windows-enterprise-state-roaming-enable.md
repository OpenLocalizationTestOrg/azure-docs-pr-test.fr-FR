---
title: aaaEnable Enterprise State Roaming dans Azure Active Directory | Documents Microsoft
description: "Foire aux questions sur les paramètres Enterprise State Roaming sur les appareils Windows. Enterprise State Roaming fournit aux utilisateurs une expérience unifiée sur leurs appareils Windows et réduit le temps de hello nécessaire pour la configuration d’un nouveau périphérique."
services: active-directory
keywords: "État entreprise itinérance cloud de windows, comment tooenable enterprise état itinérant"
documentationcenter: 
author: tanning
manager: femila
editor: curtand
ms.assetid: f71d66fd-7f9e-45eb-9cfe-5d989870f8a4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/08/2017
ms.author: markvi
ms.openlocfilehash: c69a9cfa8055f418a3b81c62939885d5bec8a6f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-enterprise-state-roaming-in-azure-active-directory"></a>Activer Enterprise State Roaming dans Azure Active Directory
Enterprise State Roaming est organisation tooany disponibles avec un abonnement Premium Azure Active Directory (Azure AD). Pour plus d’informations sur la façon de tooget un abonnement Azure AD, consultez hello [page de produit Azure AD](https://azure.microsoft.com/services/active-directory).

Lorsque vous activez Enterprise State Roaming, votre organisation sera automatiquement accordée licences pour un abonnement gratuit et limitations d’utilisation de tooAzure Rights Management. Cet abonnement gratuit est limité tooencrypting et le déchiffrement des paramètres d’entreprise et données d’application synchronisées par hello Enterprise State Roaming service ; Vous devez disposer d’un abonnement payant toouse hello toutes les fonctionnalités de gestion des droits Azure.

Après avoir obtenu un abonnement Premium d’Azure AD, suivez ces tooenable étapes Enterprise State Roaming :

1. Connexion toohello portail Azure classic.
2. Sur hello gauche, sélectionnez **ACTIVE DIRECTORY**, puis sélectionnez le répertoire hello pour lequel vous souhaitez tooenable Enterprise State Roaming.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming.png)
3. Accédez toohello **configurer** onglet en haut de hello.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-configure.png)
4. Faites défiler vers le bas de la page de hello et sélectionnez **les utilisateurs peuvent synchroniser les paramètres et données d’application ENTERPRISE**, puis cliquez sur **enregistrer**.
   ![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-select-all-sync-settings.png)

Pour un périphérique Windows 10 tooroam des paramètres avec hello Enterprise State Roaming de service, les appareils hello doivent s’authentifier à l’aide d’une identité Azure AD. Pour les appareils qui sont jointe tooAzure AD, hello principal utilisateur est l’identité de hello Azure AD, par conséquent aucune configuration supplémentaire n’est nécessaire. Pour les périphériques qui utilisent un Active Directory locale traditionnelle, hello administrateur informatique doit [connecter hello tooAzure de périphériques joints au domaine Active Directory pour Windows 10 rencontre](active-directory-azureadjoin-devices-group-policy.md).

## <a name="sync-data-storage"></a>Stockage des données de synchronisation
Enterprise State Roaming les données sont hébergées dans un ou plusieurs [régions Azure](https://azure.microsoft.com/regions/) que mieux s’aligne avec la valeur de pays/région de hello définie dans l’instance d’Azure Active Directory hello. Les données Enterprise State Roaming sont partitionnées selon les trois principales régions : Amérique du Nord, EMEA et Asie-Pacifique. Enterprise State Roaming des données pour le client de hello est localement sur le même emplacement géographique hello et ne sont pas répliquées entre les régions.  Par exemple, les clients qui ont leur tooone du jeu de valeur pays/région de pays de la région EMEA comme « France » ou « Zambie » auront leurs données hébergés dans un ou de hello régions Azure au sein de l’Europe.  Utilisateurs de définir leur valeur de pays/région dans tooone Azure AD de l’Amérique du Nord pays comme « United States » ou « Canada » auront leurs données hébergées dans un ou plusieurs des hello régions Azure dans hello des États-Unis.  Les utilisateurs de définir leur valeur de pays/région dans tooone Azure AD de pays de l’Asie-Pacifique comme « Australie » ou « Nouvelle-Zélande » auront leurs données hébergées dans un ou plusieurs des hello régions Azure au sein de l’Asie.  Amérique du Sud et les données Antarctique seront hébergées dans un ou plusieurs régions Azure dans hello des États-Unis.  valeur de pays/région Hello est définie dans le cadre de processus de création de répertoire Azure AD de hello et ne peut pas être modifiée par la suite. 

Pour plus d’informations sur l’emplacement de stockage des données, veuillez soumettre un ticket au [support technique Azure](https://azure.microsoft.com/support/options/).

## <a name="manage-enterprise-state-roaming"></a>Gérer Enterprise State Roaming
Un administrateur global Azure AD peut activer et désactiver Enterprise State Roaming Bonjour portail Azure classic.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-manage.png)

Les administrateurs globaux peuvent limiter les groupes de sécurité de toospecific de synchronisation des paramètres.

Administrateurs généraux peuvent également afficher un rapport d’état par utilisateur périphérique synchronisation en sélectionnant un utilisateur particulier dans une instance d’Active Directory hello **utilisateurs** liste et en cliquant sur **périphériques** onglet et en sélectionnant la vue **Périphériques de paramètres de synchronisation et données d’application enterprise**.
![](./media/active-directory-enterprise-state-roaming/active-directory-enterprise-state-roaming-device-sync-settings.png)

## <a name="data-retention"></a>Conservation des données
TooAzure données synchronisées via Enterprise State Roaming est conservée indéfiniment, sauf si une opération de suppression manuelle ou données hello en question sont déterminé toobe obsolètes. 

**Suppression explicite :** les données de salutation sont supprimées lorsqu’un administrateur Azure supprime un utilisateur ou un répertoire ou un administrateur demande explicitement que les données sont toobe supprimé.

* **Suppression d’un utilisateur**: lorsqu’un utilisateur est supprimé dans Azure AD, compte d’utilisateur hello itinérance des données est marquée pour suppression et sera supprimé entre too180 des 90 derniers jours. 
* **Suppression d’un répertoire**: la suppression d’un répertoire entier dans Azure AD est une opération à effet immédiat. Toutes les données de paramètres hello associée à qui active est marquée pour suppression et sera supprimé entre too180 des 90 derniers jours. 
* **Sur la suppression des demandes**: si hello Azure AD administrateur veut toomanually supprime des données ou les paramètres d’un utilisateur spécifique, hello admin peut remettre un ticket au [prise en charge Azure](https://azure.microsoft.com/support/). 

**Périmées de suppression des données**: les données qui n’ont pas été utilisées pour une année (« période de rétention hello ») sera traitée comme périmée et peut être supprimée d’Azure. période de rétention Hello est sujet toochange mais ne sera pas inférieur à 90 jours. les données obsolètes Hello peuvent être un ensemble de paramètres d’application/Windows ou de tous les paramètres pour un utilisateur spécifique. Par exemple :

* Si aucun appareil accéder à une collection de paramètres particulier (par exemple, une application est supprimée de l’appareil de hello ou un groupe de paramètres tels que « Thème » est désactivé pour tous les périphériques d’un utilisateur), puis ce regroupement deviennent obsolète après la période de rétention hello et peut être supprimé. 
* Si un utilisateur a désactivé de la synchronisation des paramètres sur tous les appareils de son, puis aucune des données de paramètres hello est accessible et toutes les données de paramètres hello pour cet utilisateur deviendront obsolètes et peuvent être supprimées après la période de rétention hello. 
* Si l’administrateur Active hello Azure AD désactive Enterprise State Roaming hello tout le répertoire, puis tous les utilisateurs dans ce répertoire s’arrêtera la synchronisation des paramètres et toutes les données de paramètres pour tous les utilisateurs deviendront obsolètes et peuvent être supprimées après la période de rétention hello. 

**Récupération de données supprimés**: stratégie de rétention de données hello n’est pas configurable. Une fois que les données de salutation a été définitivement supprimées, il ne sera pas récupérable. Toutefois, il est important de toonote qui hello des données de paramètres est supprimé uniquement à partir d’Azure, pas le périphérique de l’utilisateur final hello. Si n’importe quel appareil se connecte de nouveau service d’Enterprise State Roaming toohello, les paramètres de hello seront à nouveau être synchronisés et stockées dans Azure.

## <a name="related-topics"></a>Rubriques connexes
* [Présentation d’Enterprise State Roaming](active-directory-windows-enterprise-state-roaming-overview.md)
* [FAQ sur l’itinérance des paramètres et des données](active-directory-windows-enterprise-state-roaming-faqs.md)
* [Paramètres de stratégie de groupe et de MDM pour la synchronisation des paramètres](active-directory-windows-enterprise-state-roaming-group-policy-settings.md)
* [Référence des paramètres d’itinérance Windows 10](active-directory-windows-enterprise-state-roaming-windows-settings-reference.md)
* [Dépannage](active-directory-windows-enterprise-state-roaming-troubleshooting.md)
