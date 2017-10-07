---
title: aaaHow toouse hello Azure Active Directory Power Pack de contenu BI | Documents Microsoft
description: "Découvrez comment toouse hello Azure Active Directory Power Pack de contenu BI"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d07d678aedbe3089c4ea5f981f72311bdb389a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-active-directory-power-bi-content-pack"></a>Comment toouse hello Azure Active Directory Power Pack de contenu BI

Comprendre comment vos utilisateurs adoptent et utilisent les fonctionnalités d’Azure Active Directory est essentiel pour vous en tant qu’administrateur informatique. Il vous permet de tooplan votre utilisation de l’informatique infrastructure et la communication du tooincrease et de tooget hello plus parti des fonctionnalités d’AAD. Pack de contenu de Power BI pour Azure Active Directory donne hello de capacité toofurther analyse votre toounderstand données comment vous pouvez utiliser cette analyses plus riches toogather de données en ce qui se passe leur annuaire Active Directory de Azure pour hello différentes fonctionnalités vous fortement s’appuient sur.  Avec l’intégration de hello d’Azure Active Directory API dans Power BI, vous pouvez facilement télécharger les packs de contenu prédéfinis hello et exploiter les activités de hello tooall dans Azure Active Directory à l’aide d’expérience de visualisation riches de que Power BI offre. Vous pouvez créer votre propre tableau de bord et le partager facilement avec d’autres personnes de votre organisation. 

Cette rubrique fournit des instructions détaillées sur comment tooinstall et utilisez hello contenu pack dans votre environnement.

## <a name="installation"></a>Installation  

**hello tooinstall Pack de contenu Power BI :**

1. Connectez-vous à [Power BI](https://app.powerbi.com/groups/me/getdata/services) avec votre compte Power BI (il s’agit de hello même compte que votre Office 365 ou Azure AD).

2. Au bas de hello hello gauche du volet de navigation, sélectionnez **obtenir des données**.

    ![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. Bonjour **Services** , cliquez sur **obtenir**.
   
    ![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  Recherchez **Azure Active Directory**.

    ![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  Lorsque vous y êtes invité, tapez votre ID client Azure AD, puis cliquez sur **Suivant**.

    > [!TIP] 
    > Un Bonjour de tooget rapidement des Id de client pour votre client Office 365 / Azure AD est toologin toohello portail Azure AD, Descendre toohello active et copier hello ID à partir de hello suivant URL : https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ ActiveDirectoryExtension/répertoire/<tenantid>/directoryQuickStart

    ![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  Cliquez sur **Se connecter**. 
 
    ![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  Entrez votre nom d’utilisateur et un mot de passe, puis cliquez sur **Se connecter**.
 
    ![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  Dans la boîte de dialogue hello application consentement, cliquez sur **accepter**.
 
9.  Une fois le tableau de bord des journaux Azure Active Directory créé, cliquez dessus.
 
    ![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a>Que puis-je faire avec ce pack de contenu ?

Avant que nous passons ce que vous pouvez faire avec ce pack de contenu, l’aperçu rapide de hello Voici différents rapports dans le contenu de hello pack. Rapports de données repasse toohello **30 derniers jours**.

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a>Rapports inclus dans cette version du pack de contenu de journaux Azure Active Directory

**État de l’utilisation des applications et de tendance**: obtenir des informations sur les applications hello utilisées dans votre organisation et celles qui est utilisées hello plus et à quel moment. Vous pouvez utiliser ce rapport toogather appréhender comment une application qui vous a récemment déployé dans votre organisation est utilisée ou savoir quelles applications sont populaires. Ce faisant, vous pouvez améliorer l’utilisation si vous voyez si application hello n’est pas utilisée.

**Connexions par emplacement et les utilisateurs**: obtenir des informations sur tous les hello connexions effectuées à l’aide de l’identité et Azure fournit des informations en identité hello d’utilisateurs de hello. Cette option permet d’examiner de manière plus approfondie les connexions individuelles et de répondre aux questions telles que :

- À partir de quel endroit l’utilisateur s’est-il connecté ?
- Les utilisateurs qui ont hello la plupart des connexions et où leur connexion à l’aide de ? 
- Réussite de hello connectez-vous ?  
 
Vous pouvez parcourir les informations en cliquant sur une date ou un emplacement spécifique.

**Utilisateurs uniques par application** : pour obtenir une vue de l’ensemble des utilisateurs uniques à l’aide d’une application donnée. Cela comprend uniquement les utilisateurs qui se sont connectés « *avec succès* » à une application.

**Les connexions d’appareil**: obtenir une vue de type hello du système d’exploitation et navigateurs utilisés par les utilisateurs de votre organisation avec des informations détaillées sur les utilisateurs de hello, notamment :

- User Name
- Adresse IP
- Lieu 
- État de la connexion 

Avec ce rapport, vous pouvez comprendre hello différents profils d’appareils utilisés au sein de votre organisation et déterminent les stratégies de périphérique en fonction de ce qui est utilisé

**Synthèse SSPR** : pour comprendre le fonctionnement de la réinitialisation des mots de passe de votre organisation. Obtenir un aperçu en combien mot de passe réinitialise a été tentée via l’outil SSPR hello et nombre d'entre eux aboutit réussi. Approfondissez Échec de réinitialisation de mot de passe hello à l’aide de la forme d’entonnoir SSPR hello et comprendre pourquoi certains échecs se sont produites. Ce rapport fournit une bonne compréhension de la manière d’utiliser hello SSPR outil au sein de votre organisation afin de prendre les décisions informées hello.

## <a name="customizing-azure-ad-activity-content-pack"></a>Personnalisation du pack de contenu d’activité Azure AD

**Modifier la visualisation**: vous pouvez modifier une visualisation de rapport en cliquant sur **modifier le rapport** et sélectionnez la visualisation hello voulue.
 
![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

**Inclure des champs supplémentaires**: vous pouvez ajouter un rapport de toohello de champ ou supprimez-le en sélectionnant les toowhich visual hello tooadd/supprimer hello champ. Dans l’exemple hello ci-dessous, j’ajoute « état de la connexion » champ toohello vue table. 
 
![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

**Tableau de bord de code confidentiel visualisations tooyour**: vous pouvez personnaliser votre tableau de bord et inclure votre propre rapport toohello de visualisations et épingler toohello le tableau de bord. Dans l’exemple hello ci-dessous, j’ai ajouté un nouveau filtre appelé « état de la connexion » et inclus dans le rapport de hello. J’également modifié de visualisation de hello de graphique en courbes tooa graphique à barres et que vous pouvez épingler ce nouveau tableau de bord toohello visual.

![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


**Partager votre tableau de bord**: une fois que vous avez créé le contenu hello souhaité, vous pouvez partager du tableau de bord hello avec des utilisateurs hello dans votre organisation. N’oubliez pas qu’une fois que vous partagez des rapports de hello, ils peuvent voir les champs hello que vous avez sélectionné dans le rapport de hello.
 
![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a>Planification d’une actualisation quotidienne de votre rapport Power BI

tooschedule une actualisation quotidienne de votre rapport Power BI, accédez trop**jeux de données > Paramètres > planifier l’actualisation** et définissez-le comme indiqué ci-dessous.
 
![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-toonewer-version-of-content-pack"></a>Mise à jour de la version toonewer du pack de contenu

Si vous souhaitez tooupdate votre pack de contenu tooget une version plus récente :

- Télécharger le nouveau pack de contenu hello et configurez-le conformément aux instructions figurant dans cet article.

- Une fois que vous avez configuré il, consultez trop**Source de données > Paramètres > informations d’identification de source de données** et entrer à nouveau vos informations d’identification comme indiqué ci-dessous

    ![Pack de contenu Power BI Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

Dès que hello nouvelle version du pack de contenu hello fonctionne, vous pouvez supprimer l’ancienne hello si nécessaire en supprimant les rapports sous-jacents hello et jeux de données associés à ce pack de contenu.

## <a name="still-having-issues"></a>Vous rencontrez toujours des problèmes ? 

Consultez notre [guide de résolution des problèmes](active-directory-reporting-troubleshoot-content-pack.md). Pour obtenir une aide générale sur Power BI, consultez ces [articles d’aide](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).
 

## <a name="next-steps"></a>Étapes suivantes

Pour une vue d’ensemble de la création de rapports, consultez hello [reporting d’Azure Active Directory](active-directory-reporting-azure-portal.md).
