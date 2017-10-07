---
title: "Azure AD Connect : Certificat SSL hello mise à jour pour une batterie de serveurs de Services de fédération Active Directory (AD FS) | Documents Microsoft"
description: "Ce document détails hello étapes tooupdate hello certificat SSL d’une batterie de serveurs AD FS à l’aide d’Azure AD Connect."
services: active-directory
keywords: "azure ad connect, mise à jour de ssl adfs, mise à jour d’un certificat adfs, modifier un certificat adfs, nouveau certificat adfs, certificat adfs, mettre à jour un certificat ssl adf, mettre à jour un certificat adf ssl, configurer un certificat ssl adf, adfs, ssl, certificat, adfs certificat de communication de service, mettre à jour la fédération, configurer la fédération, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a>Mettre à jour le certificat SSL de hello pour une batterie de serveurs de Services de fédération Active Directory (AD FS)

## <a name="overview"></a>Vue d'ensemble
Cet article décrit comment vous pouvez utiliser le certificat SSL de Azure AD Connect tooupdate hello pour une batterie de serveurs de Services de fédération Active Directory (AD FS). Vous pouvez utiliser le certificat SSL de hello Azure AD Connect outil tooeasily mise à jour hello pour la batterie de serveurs hello AD FS même si hello utilisateur méthode de connexion sélectionné n’est pas AD FS.

Vous pouvez effectuer hello ensemble de l’opération de mise à jour le certificat SSL pour la batterie de serveurs hello AD FS sur l’ensemble de fédération et de serveurs Web Application Proxy (WAP) en trois étapes simples :

![Trois étapes](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
>toolearn en savoir plus sur les certificats utilisés par AD FS, consultez [présentation des certificats utilisés par AD FS](https://technet.microsoft.com/library/cc730660.aspx).

## <a name="prerequisites"></a>Composants requis

* **Batterie de serveurs AD FS** : Assurez-vous que votre batterie AD FS est basée sur Windows Server 2012 R2 ou version ultérieure.
* **Azure AD Connect**: Vérifiez que hello version d’Azure AD Connect est 1.1.443.0 ou version ultérieure. Vous allez utiliser la tâche hello **mise à jour AD certificat SSL FS**.

![Mettre à jour la tâche SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a>Étape 1 : Fournir les informations sur la batterie de serveurs AD FS

Azure AD Connect automatiquement par les tentatives tooobtain d’informations sur la batterie de serveurs hello AD FS :
1. Interrogation des informations de batterie de serveurs hello d’AD FS (Windows Server 2016 ou version ultérieure).
2. Référence à des informations de hello exécutions précédentes, qui sont stockés en local avec Azure AD Connect.

Vous pouvez modifier la liste hello des serveurs qui sont affichés en ajoutant ou supprimant hello serveurs tooreflect hello configuration actuelle de la batterie de serveurs hello AD FS. Dès que les informations de serveur hello sont fournies, Azure AD Connect affiche la connectivité de hello et l’état actuel du certificat SSL.

![Informations du serveur AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

Si la liste de hello contient un serveur qui ne fait plus partie de la batterie de serveurs hello AD FS, cliquez sur **supprimer** serveur hello toodelete liste hello des serveurs dans votre batterie AD FS.

![Serveur hors connexion dans la liste](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> Suppression d’un serveur à partir de la liste de hello de serveurs pour un AD FS de batterie de serveurs dans Azure AD Connect est une opération locale et les mises à jour hello concernant hello batterie AD FS qui tient à jour Azure AD Connect localement. Azure AD Connect ne modifie pas configuration hello sur AD FS tooreflect hello modification.    

## <a name="step-2-provide-a-new-ssl-certificate"></a>Étape 2 : Fournir un nouveau certificat SSL

Une fois que vous avez confirmé hello plus d’informations sur les serveurs de batterie de serveurs AD FS, Azure AD Connect demande un nouveau certificat SSL de hello. Fournir une installation de hello toocontinue protégé par mot de passe PFX certificat.

![Certificat SSL](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

Une fois que vous fournissez le certificat de hello, Azure AD Connect passe par une série de conditions préalables. Vérifiez que hello certificat tooensure qui hello certificat est correct pour la batterie de serveurs hello AD FS :

-   Bonjour nom d’objet/remplacement du nom de sujet de certificat de hello est même hello en tant que nom de service de fédération hello, ou il s’agit d’un certificat générique.
-   certificat de Hello est valide pendant plus de 30 jours.
-   chaîne d’approbation de certificat Hello est valide.
-   certificat de Hello est protégé par mot de passe.

## <a name="step-3-select-servers-for-hello-update"></a>Étape 3 : Sélectionner des serveurs de mise à jour hello

Dans l’étape suivante de hello, sélectionnez les serveurs de hello nécessitant un certificat SSL de toohave hello mis à jour. Serveurs qui sont hors connexion ne peut pas être sélectionnés pour la mise à jour hello.

![Sélectionnez des serveurs tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

Après avoir terminé la configuration de hello, Azure AD Connect affiche de message de type hello qui indique l’état de hello de mise à jour hello et fournit une option tooverify hello AD FS connectez-vous.

![Configuration terminée](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a>FAQ

* **Quelle doit être hello nom du sujet du certificat de hello hello nouveau certificat SSL AD FS ?**

    Azure AD Connect vérifie si hello/remplacement du nom du sujet nom du sujet hello certificat contient le nom de service de fédération hello. Par exemple, si le nom de votre service de fédération est fs.contoso.com, nom de l’objet de nom/autre sujet hello doit être fs.contoso.com.  Les certificats à caractères génériques sont également acceptés.

* **Pourquoi suis-je invité pour les informations d’identification à nouveau sur la page du serveur WAP hello ?**

    Si les informations d’identification de hello que vous fournissez pour la connexion des serveurs de FS tooAD n’ont également les serveurs de proxy hello privilège toomanage hello, Azure AD Connect vous demande des informations d’identification qui ont des privilèges d’administrateur sur les serveurs de proxy hello.

* **serveur de Hello est affiché en mode hors connexion. Que dois-je faire ?**

    Azure AD Connect ne peut pas effectuer une opération si hello serveur est hors connexion. Si le serveur de hello fait partie de hello batterie AD FS, puis vérifiez le serveur de toohello connectivité hello. Une fois que vous avez résolu le problème de hello, appuyez sur hello actualisation icône tooupdate hello de l’état dans l’Assistant de hello. Si le serveur de hello faisait partie de hello batterie précédemment mais maintenant n’existe plus, cliquez sur **supprimer** toodelete tient à jour de liste de hello des serveurs Azure AD Connect. Suppression de serveur hello dans liste hello dans Azure AD Connect ne modifie pas hello configuration AD FS lui-même. Si vous utilisez AD FS dans Windows Server 2016 ou version ultérieure, reste du serveur hello dans les paramètres de configuration hello et s’affichera à nouveau hello prochaine hello tâche est exécutée.

* **Puis-je mettre à jour un sous-ensemble de mes serveurs de la batterie de serveurs avec le nouveau certificat SSL de hello ?**

    Oui. Vous pouvez toujours exécuter la tâche hello **certificat SSL de mise à jour** à nouveau les hello tooupdate serveurs restant. Sur hello **sélectionnez des serveurs SSL de certificats mise à jour** page, vous pouvez trier hello liste des serveurs sur **date d’expiration de SSL** tooeasily accès hello serveurs qui ne sont pas encore mis à jour.

* **J’ai supprimé serveur hello Bonjour précédente exécution, mais il est toujours affiché comme en mode hors connexion et est répertorié sur la page de serveurs ADFS hello AD. Pourquoi est-il toujours les serveur hors connexion hello même après la suppression d’il ?**

    Suppression de serveur hello dans liste hello dans Azure AD Connect ne supprime Bonjour configuration AD FS. Azure AD Connect fait référence à AD FS (Windows Server 2016 ou version ultérieure) pour toutes les informations concernant la batterie de serveurs hello. Si le serveur de hello est toujours présente dans hello configuration AD FS, il sera répertorié dans la liste de hello.  

## <a name="next-steps"></a>Étapes suivantes

- [Fédération avec Azure AD Connect](active-directory-aadconnectfed-whatis.md)
- [Gestion des services AD FS (Active Directory Federation Services) et personnalisation avec Azure AD Connect](active-directory-aadconnect-federation-management.md)
