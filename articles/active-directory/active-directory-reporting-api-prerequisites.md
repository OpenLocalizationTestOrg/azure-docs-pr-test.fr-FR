---
title: "API reporting aaaPrerequisites tooaccess hello Azure AD. | Microsoft Docs"
description: "En savoir plus sur les API reporting de hello conditions préalables tooaccess hello Azure AD"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>API de création de rapports conditions préalables tooaccess hello Azure AD
Hello [AD Azure reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) vous fournir des données de toohello de l’accès par programme via un ensemble d’API REST. Vous pouvez appeler ces API à partir de divers outils et langages de programmation.

Hello reporting utilise des API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) API tooauthorize toohello web à l’accès. 

tooprepare toohello de votre accès aux API de création de rapports, vous devez :

1. Créer une application dans votre client Azure AD 
2. Grant hello application les autorisations appropriées tooaccess hello données Azure AD
3. Collecter les paramètres de configuration de votre annuaire

Si vous avez des questions, des problèmes ou des commentaires, veuillez contacter [Aide à la création de rapports AAD](mailto:aadreportinghelp@microsoft.com).

## <a name="create-an-azure-ad-application"></a>Créer une application Azure AD
tooconfigure votre API directory tooaccess hello AD Azure reporting, vous devez vous connecter toohello portail classique Azure avec un compte d’administrateur d’abonnement Azure est également un membre du rôle d’annuaire hello administrateur général dans votre locataire Azure AD.

> [!IMPORTANT]
> Applications qui s’exécutent sous les informations d’identification avec des privilèges « admin », comme cela peuvent être très puissantes, donc Veuillez être des informations d’identification de l’application que tookeep hello ID/secret sécurisé.
> 
> 

1. Bonjour [portail Azure classic](https://manage.windowsazure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. À partir de hello **active directory** , sélectionnez votre annuaire.
3. Dans le menu hello haut de hello, cliquez sur **Applications**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Dans la barre inférieure de hello, cliquez sur **ajouter**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/03.png) 
5. Sur hello **comment vous souhaitez toodo ?** boîte de dialogue, cliquez sur **ajouter une application développée par mon organisation**. 
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/04.png) 
6. Sur hello **Parlez-nous de votre application** boîte de dialogue, effectuer hello comme suit : 
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    a. Bonjour **nom** zone de texte, tapez un nom (par exemple : Application de l’API Reporting).
   
    b. Sélectionnez **Application Web et/ou API Web**.
   
    c. Cliquez sur **Suivant**.
7. Sur hello **propriétés de l’application** boîte de dialogue, effectuer hello comme suit : 
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    a. Bonjour **URL de connexion** zone de texte, type `https://localhost`.
   
    b. Bonjour **URI ID d’application** zone de texte, type ```https://localhost/ReportingApiApp```.
   
    c. Cliquez sur **Terminé**.

## <a name="grant-your-application-permission-toouse-hello-api"></a>Accorder votre hello de toouse autorisation application API
1. Bonjour [portail Azure classic](https://manage.windowsazure.com/), on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. À partir de hello **active directory** , sélectionnez votre annuaire.
3. Dans le menu hello haut de hello, cliquez sur **Applications**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/02.png)
4. Dans la liste des applications hello, sélectionnez votre application nouvellement créé.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/07.png)
5. Dans le menu hello haut de hello, cliquez sur **configurer**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/08.png)
6. Bonjour **autorisations tooother applications** section, pourquoi **Azure Active Directory** ressource, cliquez sur hello **autorisations d’Application** la liste déroulante, puis Sélectionnez **lire les données d’annuaire**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/09.png)
7. Dans la barre inférieure de hello, cliquez sur **enregistrer**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a>Collecter les paramètres de configuration de votre annuaire
Cette section vous montre comment hello tooget suivant les paramètres de votre annuaire :

* Nom de domaine
* ID client
* Clé secrète client

Vous avez besoin de ces valeurs lors de la configuration d’API de création de rapports appelle toohello. 

### <a name="get-your-domain-name"></a>Obtenir votre nom de domaine
1. Bonjour [portail Azure classic](https://manage.windowsazure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. À partir de hello **active directory** , sélectionnez votre annuaire.
3. Dans le menu hello haut de hello, cliquez sur **domaines**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/11.png) 
4. Bonjour **nom de domaine** colonne, copiez votre nom de domaine.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a>Obtenir l’ID de client de l’application hello
1. Bonjour [portail Azure classic](https://manage.windowsazure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. À partir de hello **active directory** , sélectionnez votre annuaire.
3. Dans le menu hello haut de hello, cliquez sur **Applications**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Dans la liste des applications hello, sélectionnez votre application nouvellement créé.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/07.png)
5. Dans le menu hello haut de hello, cliquez sur **configurer**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/08.png)
6. Copiez votre **ID Client**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a>Obtenir la clé secrète du client de l’application hello
tooget cliente de votre application secrète, vous devez toocreate une nouvelle clé et enregistrer, sa valeur lors de l’enregistrement de clé hello, car il n’est pas possible de tooretrieve cette valeur ultérieurement plus.

1. Bonjour [portail Azure classic](https://manage.windowsazure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/01.png) 
2. À partir de hello **active directory** , sélectionnez votre annuaire.
3. Dans le menu hello haut de hello, cliquez sur **Applications**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Dans la liste des applications hello, sélectionnez votre application nouvellement créé.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/07.png)
5. Dans le menu hello haut de hello, cliquez sur **configurer**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/08.png)
6. Bonjour **clés** section, effectuer hello comme suit : 
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/14.png)
   
    a. À partir de la liste de durée hello, sélectionnez une durée
   
    b. Dans la barre inférieure de hello, cliquez sur **enregistrer**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites/10.png)
   
    c. Copiez la valeur de clé hello.

## <a name="next-steps"></a>Étapes suivantes
* Serait vous comme tooaccess hello des données à partir d’Azure AD de hello reporting API de manière programmée ? Extraire [prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).
* Si vous souhaitez que toofind plus d’informations sur la création de rapports Azure Active Directory, consultez hello [Guide Azure Active Directory Reporting](active-directory-reporting-guide.md).  

