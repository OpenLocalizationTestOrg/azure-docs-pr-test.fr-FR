---
title: "domaines aaaCustom dans le Proxy d’Application Azure AD | Documents Microsoft"
description: "Gérer les domaines personnalisés dans le Proxy d’Application Azure AD pour cette URL hello pour une application hello est hello même quelle que soit l’endroit où vos utilisateurs y accéder."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 2fe9f895-f641-4362-8b27-7a5d08f8600f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 7a433c411976077210a2435c3c087991c7430755
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-custom-domains-in-azure-ad-application-proxy"></a>Utilisation des domaines personnalisés dans le proxy d'application Azure AD

Lorsque vous publiez une application via le Proxy d’Application Azure Active Directory, vous créez une URL externe pour votre toowhen de toogo utilisateurs qu'ils travaillent à distance. Cette URL Obtient le domaine par défaut de hello *yourtenant.msappproxy.net*. Par exemple, si vous avez publié une application nommée dépenses votre client est nommé Contoso, puis les URL externe hello serait https://expenses-contoso.msappproxy.net. Si vous souhaitez toouse votre propre nom de domaine, configurez un domaine personnalisé pour votre application. 

Nous vous recommandons de définir des domaines personnalisés pour vos applications, le cas échéant. Certains des avantages de hello de domaines personnalisés sont les suivantes :

- Les utilisateurs accèdent application toohello avec hello même URL, qu’ils travaillent à l’intérieur ou à l’extérieur de votre réseau.
- Si toutes vos applications ont hello les mêmes URL internes et externes, des liens dans une application qui pointent tooanother continuent toowork même en dehors de réseau d’entreprise de hello. 
- Vous contrôler votre marque et créez des URL hello souhaité. 


## <a name="configure-a-custom-domain"></a>Configuration d’un domaine personnalisé

### <a name="prerequisites"></a>Composants requis

Avant de configurer un domaine personnalisé, assurez-vous que vous avez hello suivant les exigences préparés : 
- A [domaine vérifié ajouté tooAzure Active Directory](active-directory-domains-add-azure-portal.md).
- Un certificat personnalisé pour le domaine hello, sous forme de hello d’un fichier PFX. 
- Une application locale [publiée via le Proxy d’application](application-proxy-publish-azure-portal.md).

### <a name="configure-your-custom-domain"></a>Configurer votre domaine personnalisé

Lorsque vous avez ces trois conditions prêt, suivez ces tooset étapes de votre domaine personnalisé :

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Accédez trop**Azure Active Directory** > **des applications d’entreprise** > **toutes les applications** et choisissez l’application hello souhaité toomanage.
3. Sélectionnez **Proxy d’application**. 
4. Dans le champ URL externe de hello, utilisez tooselect de liste déroulante hello votre domaine personnalisé. Si vous ne voyez pas votre domaine dans la liste de hello, puis il n’a pas été vérifié encore. 
5. Sélectionnez **Enregistrer**.
5. Hello **certificat** champ qui a été désactivé est activé. Sélectionnez ce champ. 

   ![Cliquez sur tooupload un certificat](./media/active-directory-application-proxy-custom-domains/certificate.png)

   Si vous avez téléchargé déjà un certificat pour ce domaine, le champ certificat hello affiche des informations de certificat hello. 

6. Télécharger un certificat PFX hello et entrez un mot de passe hello hello certificat. 
7. Sélectionnez **enregistrer** toosave vos modifications. 
8. Ajouter un [enregistrement DNS](../dns/dns-operations-recordsets-portal.md) que les redirections hello nouveau domaine msappproxy.net de toohello URL externe. 

>[!TIP] 
>Vous ne devez tooupload un certificat par domaine personnalisé. Une fois que vous téléchargez un certificat, vous pouvez choisir les domaines personnalisés hello lorsque vous publiez une application et n’avez pas une configuration supplémentaire à l’exception d’un enregistrement DNS hello toodo. 

## <a name="manage-certificates"></a>Gérer des certificats

### <a name="certificate-format"></a>Format de certificat
Il n’existe aucune restriction sur les méthodes de signature de certificat hello. Chiffrement à courbe elliptique (ECC), autre nom de l’objet (SAN) et d’autres types de certificat courants sont tous pris en charge. 

Vous pouvez utiliser un certificat générique tant que hello générique correspond à l’URL externe de hello souhaité. 

Vous pouvez également utiliser des certificats auto-signés. Si vous utilisez une autorité de certification privée, hello CDP (point de distribution de point de révocation de certificats) pour le certificat de hello doit être publique.

### <a name="changing-hello-domain"></a>La modification du domaine de hello
Tous les domaines vérifiés s’affichent dans la liste de déroulante hello URL externe pour votre application. domaine de hello toochange, mettre à jour uniquement ce champ pour l’application hello. Si le domaine hello souhaité ne figure pas dans la liste hello, [ajouter en tant que d’un domaine vérifié](active-directory-domains-add-azure-portal.md). Si vous sélectionnez un domaine que vous n’avez pas encore d’un certificat associé, suivez le certificat de hello tooadd étapes 5 à 7. Ensuite, assurez-vous que vous mettez à jour hello tooredirect d’enregistrement DNS à partir de la nouvelle hello des URL externe. 

### <a name="certificate-management"></a>Gestion des certificats
Vous pouvez utiliser le même certificat pour plusieurs applications, sauf si les applications hello partagent un hôte externe de hello. 

Vous obtenez un avertissement lorsqu’un certificat expire, vous informe tooupload un autre certificat via le portail de hello. Si le certificat de hello est révoqué, vos utilisateurs peuvent voir un avertissement de sécurité lors de l’accès d’application hello. Nous n’effectuons pas de vérification pour déterminer si les certificats sont révoqués.  certificat de hello tooupdate pour une application donnée, accédez toohello application et suivez les étapes 5 à 7 pour la configuration des domaines personnalisés sur tooupload d’applications publiées un nouveau certificat. Si l’ancien certificat de hello n’est pas utilisé par d’autres applications, il est automatiquement supprimé. 

Toute la gestion des certificats est actuellement via les pages d’application individuels vous avez besoin de certificats toomanage dans le contexte hello d’applications approprié de hello. 

## <a name="next-steps"></a>Étapes suivantes
* [Activer l’authentification unique sur](active-directory-application-proxy-sso-using-kcd.md) tooyour publié des applications avec l’authentification Azure AD.
* [Activer l’accès conditionnel](active-directory-application-proxy-conditional-access.md) tooyour les applications publiées.
* [Ajouter votre tooAzure de nom de domaine personnalisé AD](active-directory-domains-add-azure-portal.md)


