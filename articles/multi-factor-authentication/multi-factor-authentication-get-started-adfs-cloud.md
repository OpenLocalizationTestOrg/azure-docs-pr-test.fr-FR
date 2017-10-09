---
title: aaaSecure des ressources de cloud avec Azure MFA et AD FS | Documents Microsoft
description: "Il s’agit de page d’authentification multifacteur Azure hello qui décrit comment tooget main d’Azure MFA et AD FS dans le cloud de hello."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 0927fc67-8090-4fdd-913a-b3cfed3fbe77
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: kgremban
ms.openlocfilehash: 8d38d6a4af63ddcaf0fefded0b73d82d5178aa36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-cloud-resources-with-azure-multi-factor-authentication-and-ad-fs"></a>Sécurisation des ressources de cloud avec le serveur Azure Multi-Factor Authentication et AD FS
Si votre organisation est fédérée avec Azure Active Directory, utilisez l’authentification multifacteur Azure ou des ressources de toosecure de Services de fédération Active Directory (AD FS) qui sont accessibles par Azure AD. Utilisez hello suivant les procédures toosecure Azure les ressources Active Directory avec Azure multi-Factor Authentication ou Active Directory Federation Services.

## <a name="secure-azure-ad-resources-using-ad-fs"></a>Sécurisation des ressources Azure AD à l’aide d’AD FS
toosecure vos ressources de cloud, configurez une règle de revendication afin que les Services de fédération Active Directory émet hello multipleauthn revendication lorsqu’un utilisateur effectue une vérification en deux étapes avec succès. Cette revendication est passée sur tooAzure AD. Suivez cette toowalk procédure étapes hello :


1. Ouvrez Gestion AD FS.
2. Sur hello gauche, sélectionnez **confiance**.
3. Cliquez avec le bouton droit sur **Plateforme d’identité Microsoft Office 365** et sélectionnez **Modifier les règles de revendication**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)

4. Sous Règles de transformation d’émission, cliquez sur **Ajouter une règle**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)

5. On hello ajouter un Assistant de règle de revendication transformer, sélectionnez **passer ou filtrer une revendication entrante** dans hello de liste déroulante, puis cliquez sur **suivant**.

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)

6. Nommez votre règle. 
7. Sélectionnez **références des méthodes d’authentification** comme hello entrants le type de revendication.
8. Sélectionnez **Transférer toutes les valeurs de revendication**.
    ![Assistant Ajouter une règle de revendication de transformation](./media/multi-factor-authentication-get-started-adfs-cloud/configurewizard.png)
9. Cliquez sur **Terminer**. Fermez la console de gestion ADFS hello AD.

## <a name="trusted-ips-for-federated-users"></a>Adresses IP de confiance pour les utilisateurs fédérés
Adresses IP approuvées permettent aux administrateurs de vérification d’en deux étapes tooby-test pour des adresses IP spécifiques, ou pour les utilisateurs fédérés qui possèdent leur propre intranet d’origine à partir de requêtes. Hello sections suivantes décrivent comment tooconfigure approuvées Azure multi-Factor Authentication avec les utilisateurs fédérés et contourner en deux étapes si la vérification une demande provient d’un intranet d’utilisateurs fédérés des adresses IP. Cela est possible en configurant les services AD FS toouse direct ou filtrer un modèle de revendication entrante avec hello type de revendication à l’intérieur d’un réseau d’entreprise.

Cet exemple utilise Office 365 pour nos approbations de la partie de confiance.

### <a name="configure-hello-ad-fs-claims-rules"></a>Configurer les règles de revendications hello AD FS
Hello première chose toodo est tooconfigure hello AD FS revendications. Créez deux règles de revendications, l’autre pour hello à l’intérieur d’un réseau d’entreprise de revendication type et l’autre pour maintenir la connexion des utilisateurs.

1. Ouvrez Gestion AD FS.
2. Sur hello gauche, sélectionnez **confiance**.
3. Cliquez avec le bouton droit sur la **Plateforme d’identité Microsoft Office 365** et sélectionnez **Modifier les règles de revendication…**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip1.png)
4. Sous Règles de transformation d’émission, cliquez sur **Ajouter une règle.**
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip2.png)
5. On hello ajouter un Assistant de règle de revendication transformer, sélectionnez **passer ou filtrer une revendication entrante** dans hello de liste déroulante, puis cliquez sur **suivant**.
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip3.png)
6. Dans hello boîte suivant tooClaim nom de la règle, nommez votre règle. Par exemple : InsideCorpNet.
7. À partir de la liste déroulante de hello, tooIncoming suivant le type de revendication, sélectionnez **à l’intérieur d’un réseau d’entreprise**.
   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip4.png)
8. Cliquez sur **Terminer**.
9. Sous Règles de transformation d’émission, cliquez sur **Ajouter une règle**.
10. On hello ajouter un Assistant de règle de revendication transformer, sélectionnez **envoyer des revendications à l’aide d’une règle personnalisée** dans hello de liste déroulante, puis cliquez sur **suivant**.
11. Dans la zone hello sous le nom de règle de revendication : entrez *signé l’utilisateurs conserver dans*.
12. Dans la zone de règle personnalisée hello, entrez :

        c:[Type == "http://schemas.microsoft.com/2014/03/psso"]
            => issue(claim = c);
    ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip5.png)
13. Cliquez sur **Terminer**.
14. Cliquez sur **Apply**.
15. Cliquez sur **OK**.
16. Fermez Gestion AD FS.

### <a name="configure-azure-multi-factor-authentication-trusted-ips-with-federated-users"></a>Configuration d'adresses IP de confiance Azure Multi-Factor Authentication avec des utilisateurs fédérés
Maintenant que les revendications hello sont en place, nous pouvons configurer des adresses IP approuvées.

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com).
2. Sur hello gauche, cliquez sur **Active Directory**.
3. Sous répertoire, sélectionnez le répertoire de hello où vous souhaitez tooset des adresses IP approuvées.
4. Dans hello active que vous avez sélectionné, cliquez sur **configurer**.
5. Dans la section de l’authentification multifacteur hello, cliquez sur **gérer les paramètres de service**.
6. Dans la page Paramètres du Service hello, sous adresses IP approuvées, sélectionnez **ignorer multi-factor-authentication pour les demandes des utilisateurs fédérés sur mon intranet**.  

   ![Cloud](./media/multi-factor-authentication-get-started-adfs-cloud/trustedip6.png)
   
7. Cliquez sur **save**.
8. Une fois les mises à jour hello ont été appliquées, cliquez sur **fermer**.

Et voilà ! À ce stade, les utilisateurs fédérés Office 365 ne doivent avoir toouse l’authentification Multifacteur lorsqu’une revendication provient d’intranet en dehors de l’entreprise hello.
