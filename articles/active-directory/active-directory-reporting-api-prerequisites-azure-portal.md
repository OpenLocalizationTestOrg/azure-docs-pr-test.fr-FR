---
title: "API de création de rapports aaaPrerequisites tooaccess hello Azure AD | Documents Microsoft"
description: "En savoir plus sur les API reporting de hello conditions préalables tooaccess hello Azure AD"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>API de création de rapports conditions préalables tooaccess hello Azure AD

Hello [AD Azure reporting API](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) vous fournir des données de toohello de l’accès par programme via un ensemble d’API REST. Vous pouvez appeler ces API à partir de divers outils et langages de programmation.

Hello reporting utilise des API [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) API tooauthorize toohello web à l’accès. 

tooget accéder aux données de rapport toohello via les API de hello, vous devez toohave d'entre hello suivant des rôles attribués :

- Lecteur de sécurité
- Administrateur de la sécurité
- Administrateur général


tooprepare toohello de votre accès aux API de création de rapports, vous devez :

1. Inscrire une application 
2. Accorder des autorisations 
3. Rassembler les paramètres de configuration 

Si vous avez des questions, des problèmes ou des commentaires, [créez un ticket de support](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).

## <a name="register-an-azure-active-directory-application"></a>Inscrire une application Azure Active Directory

Vous devez tooregister une application même si vous accédez à hello API à l’aide d’un script de création de rapports. Cela vous donne une **ID de l’Application**, qui est requis pour un appel d’autorisation, et il permet à vos jetons tooreceive de code.

tooconfigure votre API directory tooaccess hello AD Azure reporting, vous devez vous connecter toohello portail Azure avec un compte d’administrateur Azure qui est également un membre de hello **administrateur Global** rôle d’annuaire dans votre locataire Azure AD .

> [!IMPORTANT]
> Applications qui s’exécutent sous les informations d’identification avec des privilèges « admin », comme cela peuvent être très puissantes, donc Veuillez être des informations d’identification de l’application que tookeep hello ID/secret sécurisé.
> 


**tooregister une application Azure Active Directory :**

1. Bonjour [portail Azure](https://portal.azure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Sur hello **Azure Active Directory** panneau, cliquez sur **inscriptions d’application**.

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. Sur hello **inscriptions d’application** lame, dans la barre d’outils hello en haut de hello, cliquez sur **nouvelle inscription de l’application**.

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. Sur hello **créer** panneau, effectuer hello comme suit :

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    a. Bonjour **nom** zone de texte, type `Reporting API application`.

    b. Sous **Type d’application**, sélectionnez **Application web/API**.

    c. Bonjour **URL de connexion** zone de texte, type `https://localhost`.

    d. Cliquez sur **Créer**. 


## <a name="grant-permissions"></a>Accorder des autorisations 

objectif Hello de cette étape correspond à votre application toogrant **lire les données d’annuaire** autorisations toohello **Windows Azure Active Directory** API.

![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

**toogrant votre hello de toouse autorisation application API :**

1. Sur hello **inscriptions d’application** lame, dans la liste des applications hello, cliquez sur **application API de création de rapports**.

2. Sur hello **application API de création de rapports** lame, dans la barre d’outils hello en haut de hello, cliquez sur **paramètres**. 

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. Sur hello **paramètres** panneau, cliquez sur **autorisations requises**. 

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. Sur hello **autorisations requises** panneau, Bonjour **API** , cliquez sur **Windows Azure Active Directory**. 

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. Sur hello **activer l’accès** panneau, sélectionnez **lire les données d’annuaire**. 

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. Dans la barre d’outils de hello en haut de hello, cliquez sur **enregistrer**.

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a>Rassembler les paramètres de configuration 
Cette section vous montre comment hello tooget suivant les paramètres de votre annuaire :

* Nom de domaine
* ID client
* Clé secrète client

Vous avez besoin de ces valeurs lors de la configuration d’API de création de rapports appelle toohello. 

### <a name="get-your-domain-name"></a>Obtenir votre nom de domaine

**tooget votre nom de domaine :**

1. Bonjour [portail Azure](https://portal.azure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Sur hello **Azure Active Directory** panneau, cliquez sur **les noms de domaine**.

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. Copiez votre nom de domaine à partir de la liste hello des domaines.


### <a name="get-your-applications-client-id"></a>Obtenir l’ID client de l’application

**tooget ID de client de votre application :**

1. Bonjour [portail Azure](https://portal.azure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Sur hello **inscriptions d’application** lame, dans la liste des applications hello, cliquez sur **application API de création de rapports**.

3. Sur hello **application API de création de rapports** panneau, à hello **ID d’Application**, cliquez sur **cliquez sur toocopy**.

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a>Obtenir la clé secrète client de l’application
tooget cliente de votre application secrète, vous devez toocreate une nouvelle clé et enregistrer, sa valeur lors de l’enregistrement de clé hello, car il n’est pas possible de tooretrieve cette valeur ultérieurement plus.

**tooget question secrète du client de votre application :**

1. Bonjour [portail Azure](https://portal.azure.com), on hello du volet de navigation gauche, cliquez sur **Active Directory**.
   
    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Sur hello **inscriptions d’application** lame, dans la liste des applications hello, cliquez sur **application API de création de rapports**.


3. Sur hello **application API de création de rapports** lame, dans la barre d’outils hello en haut de hello, cliquez sur **paramètres**. 

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. Sur hello **paramètres** panneau, Bonjour **APIR accès** , cliquez sur **clés**. 

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. Sur hello **clés** panneau, effectuer hello comme suit :

    ![Inscription de l’application](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    a. Bonjour **Description** zone de texte, type `Reporting API`.

    b. Dans **Expire le**, sélectionnez **Dans 2 ans**.

    c. Cliquez sur **Enregistrer**.

    d. Copiez la valeur de clé hello.


## <a name="next-steps"></a>Étapes suivantes
* Serait vous comme tooaccess hello des données à partir d’Azure AD de hello reporting API de manière programmée ? Extraire [prise en main de hello API Azure Active Directory Reporting](active-directory-reporting-api-getting-started.md).
* Si vous souhaitez que toofind plus d’informations sur la création de rapports Azure Active Directory, consultez hello [Guide Azure Active Directory Reporting](active-directory-reporting-guide.md).  

