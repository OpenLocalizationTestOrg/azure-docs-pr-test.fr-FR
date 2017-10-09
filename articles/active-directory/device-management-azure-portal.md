---
title: "appareils aaaManaging à l’aide de hello portail Azure - version préliminaire | Documents Microsoft"
description: "Découvrez comment toouse hello les appareils toomanage portail Azure."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a>La gestion des appareils à l’aide de hello portail Azure, afficher un aperçu

>[!NOTE]
>Cette fonctionnalité est actuellement disponible en préversion publique. Préparez-vous à toorevert ou supprimer toutes les modifications. Hello fonctionnalité est disponible dans n’importe quel abonnement Azure Active Directory (Azure AD) au cours de la version préliminaire publique. Toutefois, lorsque la fonctionnalité de hello devient disponible de manière générale, certains aspects de la fonctionnalité de hello peuvent nécessiter un abonnement premium à Azure Active Directory.


La fonction de gestion des appareils intégrée à Azure Active Directory (Azure AD) vous permet de vous assurer que vos utilisateurs accèdent à vos ressources à partir d’appareils qui répondent à vos normes de conformité et de sécurité. 

Cette rubrique :

- Part du principe que vous êtes familiarisé avec hello [gestion toodevice de présentation dans Azure Active Directory](device-management-introduction.md)

- Fournit des informations sur la gestion de vos appareils à l’aide de hello portail Azure


appareils toomanage Bonjour portail Azure, vous devez tooclick **périphériques** Bonjour **gérer** section Bonjour Bonjour **Azure Active Directory** panneau.

![Gérer un appareil Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a>Configurer les paramètres de l’appareil

toomanage vos appareils à l’aide de hello portail Azure, ils doivent toobe inscrit ou joint tooAzure AD. En tant qu’administrateur, vous pouvez affiner le processus de hello d’enregistrement et la jonction d’appareils en configurant les paramètres de périphérique hello.

![Gérer un appareil Intune](./media/device-management-azure-portal/22.png)


panneau des paramètres de périphérique Hello vous permet de tooconfigure :

- **Les utilisateurs peuvent joindre des appareils tooAzure AD** - ce paramètres vous permet de tooselect hello les utilisateurs peuvent joindre des appareils tooAzure AD. valeur par défaut Hello est **tous les**.

- **Les administrateurs locaux supplémentaires sur Azure AD les appareils joints à un** -vous pouvez sélectionner des utilisateurs hello disposant de droits d’administrateur local sur un appareil. Les utilisateurs ajoutés ici sont ajoutés toohello *administrateurs de l’appareil* rôle dans Azure AD. Les administrateurs généraux Azure AD et les propriétaires d’appareils bénéficient de droits d’administrateur local par défaut. Cette option est une fonctionnalité d’édition premium disponible au moyen de produits tels qu’Azure AD Premium ou hello Enterprise Mobility Suite (EMS). 

- **Les utilisateurs peuvent inscrire leurs appareils auprès d’Azure AD** -vous devez tooconfigure cette toobe de périphériques tooallow paramètre inscrit auprès d’Azure AD. Si vous sélectionnez **aucun**, les appareils ne sont pas autorisées tooregister lorsqu’ils ne sont pas Azure Active Directory joint ou hybrides Azure AD est joint. L’inscription auprès de Microsoft Intune ou de la Gestion des appareils mobiles (MDM) pour Office 365 nécessite l’enregistrement de l’appareil. Si vous avez configuré l’un de ces services, l’option **TOUS** est sélectionnée et l’option **AUCUN** est désactivée.

- **Exiger l’authentification multifacteur toojoin appareils** -vous pouvez choisir si les utilisateurs sont requis tooprovide une authentification de second facteur toojoin leur tooAzure appareil AD. valeur par défaut Hello est **non**. Il est recommandé d’exiger une authentification multifacteur au moment de l’inscription d’un appareil. Avant d’activer l’authentification multifacteur pour ce service, vous devez vous assurer que l’authentification multifacteur est configurée pour les utilisateurs de hello qui inscrivent leurs appareils. Pour plus d’informations sur les services d’authentification multifacteur Azure, consultez [Bien démarrer avec l’authentification multifacteur Azure](../multi-factor-authentication/multi-factor-authentication-get-started.md). 

- **Nombre maximal d’appareils** -ce paramètre permet de tooselect hello de nombre maximal d’appareils qu’un utilisateur dans Azure AD. Si un utilisateur atteint ce quota, ils sont en mesure de tooadd des périphériques supplémentaires jusqu'à ce qu’une ou plusieurs des périphériques existants de hello sont supprimés. guillemet de périphérique Hello est comptabilisée pour tous les périphériques qui sont Azure AD joint ou Azure AD inscrit aujourd'hui. la valeur par défaut Hello est **20**.

- **Les utilisateurs peuvent synchroniser les paramètres et données d’application pour les appareils** -par défaut, ce paramètre est défini trop**NONE**. En sélectionnant des utilisateurs spécifiques ou des groupes ou tous permet de paramètres et toosync de données d’application de l’utilisateur hello sur leurs appareils Windows 10. Découvrez comment fonctionne la synchronisation dans Windows 10.
Cette option est une fonctionnalité premium disponible au moyen de produits tels qu’Azure AD Premium ou hello Enterprise Mobility Suite (EMS).
 
    ![Gérer un appareil Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a>Localiser les appareils

En tant qu’administrateur, Bonjour portail Azure, vous avez deux options toolocate inscrit et appareils joints à un :

- **Tous les appareils** Bonjour **gérer** section Hello **périphériques** panneau  

    ![Tous les appareils](./media/device-management-azure-portal/41.png)


- **Appareils** Bonjour **gérer** section d’un **utilisateur** panneau
 
    ![Tous les appareils](./media/device-management-azure-portal/43.png)



Avec ces deux options, vous pouvez consulter tooa qui :


- Vous permet de toosearch pour les appareils à l’aide du nom d’affichage hello en tant que filtre.

- Fournit une vue d’ensemble détaillée des appareils inscrits et joints

- Vous permet de tâches courantes de gestion des périphériques tooperform
   

![Tous les appareils](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a>Tâches de gestion des appareils

En tant qu’administrateur, vous pouvez gérer hello inscrit ou appareils joints à un. Cette section fournit des informations sur les tâches courantes de gestion des appareils.


**Gérer un appareil Intune** : si vous êtes un administrateur Intune, vous pouvez gérer les appareils marqués comme étant des appareils **Microsoft Intune**. Un administrateur peut voir d’autres appareils. 

![Gérer un appareil Intune](./media/device-management-azure-portal/31.png)


**Activer/Désactiver un appareil Azure AD**

tooenable ou désactiver un périphérique, vous devez toobe un administrateur global dans Azure AD. Si vous désactivez un appareil, vous l’empêchez d’accéder à vos ressources Azure AD.  Appareil de hello toodisable, vous pouvez cliquer sur *...* Cliquez sur périphérique hello pour plus d’informations.

 
![Gérer un appareil Intune](./media/device-management-azure-portal/33.png)

Désactivation d’un périphérique change d’état de hello Bonjour **activé** colonne trop**non**.

![Désactiver un appareil](./media/device-management-azure-portal/32.png)


**Supprimer un appareil Azure AD** -toodelete un appareil, vous devez toobe un administrateur global dans Azure AD.  
La suppression d’un appareil :
 
- Empêche celui-ci d’accéder à vos ressources Azure AD 

- Supprime tous les détails qui sont attachés toohello périphérique, par exemple, les clés BitLocker pour les appareils Windows  

- Est une action irréversible et donc non recommandée, sauf si elle est absolument nécessaire

Si un appareil est géré par une autre autorité de gestion (par exemple, Microsoft Intune), assurez-vous que cet appareil hello a été réinitialisé / mis hors service avant de supprimer un périphérique de hello dans Azure AD.

Vous pouvez cliquer sur « … » toodelete hello périphérique ou cliquez sur périphérique hello pour plus d’informations
 
![Suppression d’un appareil](./media/device-management-azure-portal/34.png)


**Afficher ou copier des ID de périphérique** -vous pouvez utiliser un périphérique ID tooverify hello périphérique ID plus d’informations sur les appareils hello ou à l’aide de PowerShell lors du dépannage. tooaccess hello copie, cliquez sur le périphérique de hello.

![Afficher un ID d’appareil](./media/device-management-azure-portal/35.png)
  

**Afficher ou copier les clés BitLocker** -si vous êtes un administrateur, vous pouvez afficher et hello de copie BitLocker clés toohelp utilisateurs toorecover leur lecteur chiffré. Ces clés sont uniquement disponibles pour les appareils Windows chiffrés dont les clés sont stockées dans Azure AD. Vous pouvez copier ces clés lorsque vous accédez aux détails d’appareil de hello.
 
![Afficher les clés BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a>Journaux d’audit


activités de périphérique Hello sont disponibles via les journaux d’activité hello. Cela inclut les activités déclenchées par le service d’inscription de périphérique hello ou par l’utilisateur de hello :

- La création de périphérique et en ajoutant les utilisateurs/propriétaires d’appareil de hello

- Modifie les paramètres toodevice

- Opérations concernant les appareils, telles que la suppression ou la mise à jour d’un appareil
 
Votre toohello de point d’entrée l’audit des données est **journaux d’Audit** Bonjour **activité** section Hello **périphériques* panneau.

![Journaux d’audit](./media/device-management-azure-portal/61.png)


Un journal d’audit inclut un mode Liste par défaut, qui indique :

- date de Hello et l’heure de l’occurrence de hello

- cibles de Hello

- Hello initiateur / acteur (qui) d’une activité

- activité Hello (quoi)

![Journaux d’audit](./media/device-management-azure-portal/63.png)

Vous pouvez personnaliser l’affichage de liste hello en cliquant sur **colonnes** dans la barre d’outils hello.
 
![Journaux d’audit](./media/device-management-azure-portal/64.png)


toonarrow bas hello signalés au niveau de tooa de données que fonctionne pour vous, vous pouvez filtrer les données d’audit hello hello suivant des champs à l’aide de :

- Catégorie
- Type de ressource d’activité
- Activité
- Plage de dates
- Cible
- Initié par (intervenant)

En outre toohello filtres, vous pouvez rechercher des entrées spécifiques.

![Journaux d’audit](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a>Étapes suivantes

* [Gestion de toodevice introduction dans Azure Active Directory](device-management-introduction.md)



