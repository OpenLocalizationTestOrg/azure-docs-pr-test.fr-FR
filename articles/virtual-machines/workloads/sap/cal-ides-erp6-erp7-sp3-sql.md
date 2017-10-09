---
title: aaaDeploy SAP IDE EHP7 SP3 pour la version 6.0 de ERP SAP sur Azure | Documents Microsoft
description: "Déploiement de SAP IDES EHP7 SP3 pour SAP ERP 6.0 sur Azure"
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a>Déploiement de SAP IDES EHP7 SP3 pour SAP ERP 6.0 sur Azure
Cet article décrit comment toodeploy un SAP IDE fonctionnant avec SQL Server et le système d’exploitation de Windows hello sur Azure via hello bibliothèque de matériel du Cloud SAP (SAP CAL) 3.0. captures d’écran Hello montrent étape par étape hello. toodeploy une autre solution, suivez hello les mêmes étapes.

toostart avec hello SAP licences d’accès client, accédez toohello [SAP Cloud application bibliothèque](https://cal.sap.com/) site Web. SAP possède également un blog sur hello nouvelle [SAP Cloud Appliance bibliothèque 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience). 

> [!NOTE]
Comme de 29 mai 2017, vous pouvez utiliser le modèle de déploiement du Gestionnaire de ressources Azure hello en outre toohello préféré au moins un déploiement classique de modèle toodeploy hello licences d’accès client SAP. Nous vous recommandons d’utiliser le nouveau modèle de déploiement Resource Manager hello et de ne pas tenir compte de modèle de déploiement classique hello.

Si vous déjà créé un compte SAP licences d’accès client qui utilise le modèle classique de hello, *vous devez toocreate un autre compte de licences d’accès client SAP*. Ce compte doit tooexclusively déployer dans Azure à l’aide du modèle de gestionnaire de ressources hello.

Après vous être connecté toohello licence d’accès client SAP, première page de hello vous conduit généralement toohello **Solutions** page. solutions Hello proposées sur hello SAP licences d’accès client sont en augmentation, donc vous devrez peut-être tooscroll mal les solutions hello toofind vous souhaitez. solution IDE de SAP basés sur Windows Hello mis en surbrillance est exclusivement disponible sur Azure décrit les processus de déploiement hello :

![Solutions SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a>Créer un compte dans hello licences d’accès client SAP
1. toosign dans toohello SAP CAL pour hello première fois, utilisez votre utilisateur S SAP ou autre utilisateur enregistré dans SAP. Définissez ensuite un compte d’accès client SAP qui est utilisé par les appareils de toodeploy hello licences d’accès client SAP sur Azure. Dans la définition du compte de hello, vous devez :

    a. Sélectionnez le modèle de déploiement hello sur Azure (Gestionnaire de ressources ou classique).

    b. Entrez votre abonnement Azure. Abonnement tooone uniquement peut être affecté à un compte de la licence d’accès client SAP. Si vous avez besoin de plus d’un abonnement, vous devez toocreate un autre compte de licences d’accès client SAP.
    
    c. Donnez à hello SAP CAL autorisation toodeploy dans votre abonnement Azure.

    > [!NOTE]
    les étapes suivantes Hello montrent comment toocreate une licence d’accès client SAP compte pour les déploiements de gestionnaire de ressources. Si vous avez déjà un compte de licence d’accès client SAP qui est le modèle de déploiement classique toohello lié, vous *devez* toofollow ces toocreate étapes un nouveau compte de licences d’accès client SAP. nouveau compte de licences d’accès client SAP Hello doit toodeploy dans le modèle de gestionnaire de ressources hello.

2. toocreate une licence d’accès client SAP nouveau compte, hello **comptes** page affiche deux possibilités pour Azure : 

    a. **Microsoft Azure (classique)** est le modèle de déploiement classique hello et n’est plus recommandée.

    b. **Microsoft Azure** est le nouveau modèle de déploiement Resource Manager hello.

    ![Comptes SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    toodeploy dans le modèle de gestionnaire de ressources hello, sélectionnez **Microsoft Azure**.

    ![Comptes SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. Entrez hello Azure **ID d’abonnement** qui se trouvent sur hello portail Azure. 

    ![ID d’abonnement SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. toodeploy de licences d’accès client SAP tooauthorize hello en hello abonnement Azure que vous avez définies, cliquez sur **Authorize**. Hello suivant page s’affiche dans l’onglet du navigateur hello :

    ![Connexion aux services cloud d’Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. Si plusieurs utilisateurs est répertorié, choisissez le compte Microsoft hello coadministrator de hello toobe lié Hello abonnement Azure que vous avez sélectionné. Hello suivant page s’affiche dans l’onglet du navigateur hello :

    ![Confirmation des services cloud d’Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. Cliquez sur **Accepter**. Si l’autorisation de hello est réussie, hello définition du compte de licences d’accès client SAP s’affiche à nouveau. Après une courte période, un message confirme que le processus d’autorisation de hello a réussi.

7. tooassign hello nouvellement créée tooyour utilisateur du compte de licences d’accès client SAP, entrez votre **ID utilisateur** dans hello de zone de texte hello droit et cliquez sur **ajouter**. 

    ![Association de compte toouser](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. Cliquez sur votre compte utilisateur de hello utiliser toosign dans toohello SAP licences d’accès client, de tooassociate **révision**. 

9. association de hello toocreate entre votre utilisateur et le compte de licences d’accès client SAP hello nouvellement créé, cliquez sur **créer**.

    ![Association tooaccount utilisateur](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

Vous avez correctement créé un compte SAP CAL capable d’effectuer les tâches suivantes :

- Utilisez le modèle de déploiement du Gestionnaire de ressources hello.
- Déployer des systèmes SAP dans votre abonnement Azure.

> [!NOTE]
Avant de pouvoir déployer des solutions SAP IDE hello basée sur Windows et SQL Server, vous devrez peut-être toosign pour un abonnement de licence d’accès client SAP. Dans le cas contraire, les solutions hello risquent d’apparaître en tant que **verrouillé** sur la page de vue d’ensemble de hello.

### <a name="deploy-a-solution"></a>Déployer une solution
1. Après avoir configuré un compte de la licence d’accès client SAP, sélectionnez **hello solution SAP IDE sur Windows et SQL Server** solution. Cliquez sur **création d’une Instance**et vérifiez les conditions d’utilisation et les termes du contrat de hello. 

2. Sur hello **Mode de base : création d’une Instance** page, vous devez :

    a. Entrez une instance **Nom**.

    b. Sélectionnez une région Azure dans le champ **Region** (Région). Vous devrez peut-être une tooget d’abonnement de licence d’accès client SAP plusieurs régions Azure proposées.

    c.  Entrez le masque de hello **mot de passe** solution hello, comme indiqué :

    ![Mode de base SAP CAL : créer une instance](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. Cliquez sur **Créer**. Après un certain temps, selon la taille de hello et la complexité de la solution de hello (licence d’accès client SAP fournit une estimation hello), hello état est affiché comme actif et prêt à être utilisé : 

    ![Instances SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. groupe de ressources toofind hello et tous ses objets qui ont été créés par hello des licences d’accès client SAP, accédez toohello portail Azure. machine virtuelle de Hello sont accessibles en commençant par le même nom qui a été fourni en hello SAP licences d’accès client de l’instance de hello.

    ![Objets du groupe de ressources](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. Sur le portail de licences d’accès client SAP hello, accédez toohello déployé instances, puis cliquez sur **connexion**. Hello suivant la fenêtre contextuelle s’affiche : 

    ![Se connecter toohello Instance](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. Avant de pouvoir utiliser un des systèmes de toohello déployé tooconnect hello options, cliquez sur **Getting Started Guide**. noms de documentation Hello hello utilisateurs pour chacune des méthodes de connectivité hello. les mots de passe Hello pour les utilisateurs sont définies de mot de passe principal toohello que vous avez défini au début de hello hello du processus de déploiement. Dans la documentation de hello, les autres utilisateurs plus fonctionnelles sont répertoriés avec leur mot de passe, vous pouvez utiliser toosign dans toohello déployé le système.

    ![Documentation de présentation de SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

En quelques heures, un système SAP IDES sain est déployé dans Azure.

Si vous avez acheté un abonnement de licence d’accès client SAP, SAP prend entièrement en charge déploiements au travers de hello licences d’accès client SAP sur Azure. file d’attente de la prise en charge Hello est BC-VCM-licences d’accès client.

