---
title: "actifs d’Azure CDN aaaSecuring avec l’authentification des jetons | Documents Microsoft"
description: "À l’aide de l’authentification des jetons toosecure accès à tooyour Azure CDN des ressources."
services: cdn
documentationcenter: .net
author: zhangmanling
manager: zhangmanling
editor: 
ms.assetid: 837018e3-03e6-4f9c-a23e-4b63d5707a64
ms.service: cdn
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/11/2016
ms.author: mezha
ms.openlocfilehash: 5865bcb8eed7ced834970d52d30136252039265f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="securing-azure-cdn-assets-with-token-authentication"></a>Sécurisation des ressources CDN Azure avec l’authentification du jeton

[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

##<a name="overview"></a>Vue d'ensemble

L’authentification de jeton est un mécanisme qui vous permet de tooprevent CDN Azure prennent en charge des clients de toounauthorized actifs.  En général, cela tooprevent « hotlinking » du contenu, où un autre site Web, souvent un panneau de messages, utilise vos éléments multimédias sans autorisation.  ce qui peut avoir un impact sur les coûts de distribution de votre contenu. En activant cette fonctionnalité sur le CDN, les demandes seront authentifiées par le bord CDN POP avant la diffusion de contenu hello. 

## <a name="how-it-works"></a>Fonctionnement

L’authentification des jetons vérifie les demandes sont générées par un site de confiance en demandant à une valeur de jeton contenant les informations encodées de demandeur de hello toocontain des demandes. Le contenu sera uniquement être pris en charge toorequester lorsque hello codés besoins hello satisfait, sinon les demandes seront refusées. Vous pouvez configurer exigence hello à l’aide d’un ou plusieurs paramètres ci-dessous.

- Pays : pour autoriser ou refuser les demandes provenant des pays spécifiés.  [Liste des codes de pays valides.](https://msdn.microsoft.com/library/mt761717.aspx) 
- URL : autoriser uniquement les toorequest actif ou le chemin d’accès spécifié.  
- Hôte : autoriser ou refuser les demandes à l’aide d’ordinateurs hôtes indiqués dans l’en-tête de demande hello.
- Point d’accès : autoriser ou refuser le toorequest de point d’accès spécifié.
- Adresse IP : pour autoriser uniquement les demandes provenant d’une adresse ou d’un sous-réseau IP spécifique.
- Protocole : autoriser ou bloquer les demandes selon le protocole de hello son utilisation toorequest hello.
- Délai d’expiration : assigner une date et l’heure de période tooensure qu’un lien reste uniquement la valide pour une durée limitée.

Consultez l’exemple de configuration détaillée de chaque paramètre.

## <a name="reference-architecture"></a>Architecture de référence

Voir ci-dessous une architecture de référence de configuration de l’authentification des jetons sur toowork CDN avec votre application Web.

![Bouton de gestion du panneau de profil CDN](./media/cdn-token-auth/cdn-token-auth-workflow2.png)

## <a name="token-validation-logic-on-cdn-endpoint"></a>Logique de validation de jeton sur le point de terminaison CDN
    
Ce graphique décrit comment le CDN Azure valide la demande du client lorsque l’authentification du jeton est configurée sur le point de terminaison CDN.

![Bouton de gestion du panneau de profil CDN](./media/cdn-token-auth/cdn-token-auth-validation-logic.png)

## <a name="setting-up-token-authentication"></a>Configuration de l’authentification du jeton

1. À partir de hello [portail Azure](https://portal.azure.com), recherchez le profil CDN tooyour, puis cliquez sur hello **gérer** portail supplémentaire du bouton toolaunch hello.

    ![Bouton de gestion du panneau de profil CDN](./media/cdn-rules-engine/cdn-manage-btn.png)

2. Placez le curseur sur **grand HTTP**, puis cliquez sur **Auth jeton** dans le menu volant des hello. Vous allez configurer la clé de chiffrement et les paramètres de chiffrement dans cet onglet.

    1. Entrez une clé de chiffrement unique sous **Clé primaire**.  Entrez un autre clé sous **Backup Key** (Clé de sauvegarde)

        ![Clé de configuration de l’authentification du jeton CDN](./media/cdn-token-auth/cdn-token-auth-setupkey.png)
    
    2. Définissez les paramètres de chiffrement à l’aide de l’outil de chiffrement (autorisez ou refusez les demandes en fonction de l’heure d’expiration, du pays, du référent, du protocole ou de l’IP du client. Vous pouvez combiner ces exigences comme vous le souhaitez.)

        ![Bouton de gestion du panneau de profil CDN](./media/cdn-token-auth/cdn-token-auth-encrypttool.png)

        - ec-expire : attribue un délai d’expiration spécifique à un jeton. Demandes soumises après que l’heure d’expiration de hello sera refusé. Ce paramètre utilise l’horodatage Unix (basé sur le nombre de secondes à partir de l’époque standard 01/01/1970 00:00:00 GMT. Vous pouvez utiliser les outils en ligne tooprovide de conversion entre Unix heure et.)  Par exemple, si vous souhaitez tooset des toobe de jeton hello a expiré à 31/12/2016 12:00:00 GMT, utilisez hello Unix temps : 1483185600 comme indiqué ci-dessous :
    
        ![Bouton de gestion du panneau de profil CDN](./media/cdn-token-auth/cdn-token-auth-expire2.png)
    
        - Autoriser EC-url : vous permet d’élément multimédia en particulier tootailor jetons tooa ou chemin d’accès. Elle restreint toorequests accès dont l’URL démarrer avec un chemin d’accès relatif spécifique. Vous pouvez entrer plusieurs chemins d’accès en les séparant par une virgule. Les URL sont sensibles à la casse. Selon la spécification de hello, vous pouvez configurer différents valeur tooprovide différents niveaux d’accès. Voici quelques scénarios :
        
            Si votre URL est la suivante : http://www.mydomain.com/pictures/city/strasbourg.png. Définissez la valeur d’entrée « » et son niveau d’accès en conséquence

            1. Valeur d’entrée « / » : toutes les demandes sont autorisées
            2. Valeur d’entrée « / images » : tous les hello suivant des demandes autorisera
            
                - http://www.mydomain.com/pictures.png
                - http://www.mydomain.com/pictures/city/strasbourg.png
                - http://www.mydomain.com/picturesnew/city/strasbourgh.png
            3. Valeur d’entrée « /pictures/ » : seules les demandes pour /pictures/ sont autorisées
            4. Valeur d’entrée « /pictures/city/strasbourg.png » : seules les demandes portant sur cette ressource sont autorisées
    
        ![Bouton de gestion du panneau de profil CDN](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
    
        - ec-country-allow : autorise uniquement les demandes provenant d’un ou plusieurs pays spécifiés. Les demandes provenant d’un autre pays seront refusées. Utilisez tooset de code de pays les paramètres de hello et les séparer chaque code de pays par une virgule. Par exemple, si vous souhaitez accéder tooallow à partir des États-Unis et en France, entrée US, FR dans la colonne hello comme ci-dessous.  
        
        ![Bouton de gestion du panneau de profil CDN](./media/cdn-token-auth/cdn-token-auth-country-allow.png)

        - ec-country-deny : refuse les demandes provenant d’un ou plusieurs pays spécifiés. Les demandes provenant d’un autre pays sont autorisées. Utilisez tooset de code de pays les paramètres de hello et les séparer chaque code de pays par une virgule. Par exemple, si vous souhaitez accéder toodeny à partir des États-Unis et en France, entrée US, FR dans la colonne de hello.
    
        - ec-ref-allow : autorise uniquement les demandes provenant du référent spécifié. Un point d’accès identifie hello des URL de page web hello ressource toohello demandé a été liée. valeur du paramètre Hello point d’accès ne doit pas inclure le protocole de hello. Vous pouvez entrer un nom d’hôte et/ou un chemin d’accès particulier sur ce nom d’hôte. Vous pouvez également ajouter plusieurs référents au sein d’un même paramètre en les séparant par une virgule. Si vous avez spécifié une valeur de point d’accès, mais les informations de point d’accès hello ne sont pas envoyées dans la demande en raison de la configuration du navigateur toosome hello, ces demandes seront refusées par défaut. Vous pouvez affecter « Manquant » ou une valeur vierge dans hello paramètre tooallow ces demandes sans les informations de point d’accès. Vous pouvez également utiliser « *. consoto.com « tooallow tous les sous-domaines de consoto.com.  Par exemple, si vous souhaitez accéder tooallow pour les demandes de www.consoto.com, tous les sous-domaines sous consoto2.com et erquests avec reffers vides ou manquantes, valeur d’entrée ci-dessous :
        
        ![Bouton de gestion du panneau de profil CDN](./media/cdn-token-auth/cdn-token-auth-referrer-allow2.png)
    
        - ec-ref-deny : refuse les demandes provenant du référent spécifié. Consultez toodetails et exemple de paramètre de « ec-ref-autoriser ».
         
        - ec-proto-allow : autorise uniquement les demandes correspondant au protocole spécifié. Par exemple, http ou https.
        
        ![Bouton de gestion du panneau de profil CDN](./media/cdn-token-auth/cdn-token-auth-url-allow4.png)
            
        - ec-proto-deny : refuse les demandes correspondant au protocole spécifié. Par exemple, http ou https.
    
        - ipclient-EC : limite d’adresse IP du demandeur accès toospecified. Les adresses IPV4 et IPV6 sont prises en charge. Vous pouvez spécifier un sous-réseau IP ou une adresse IP de demande unique.
            
        ![Bouton de gestion du panneau de profil CDN](./media/cdn-token-auth/cdn-token-auth-clientip.png)
        
    3. Vous pouvez tester votre jeton avec l’outil de description hello.

    4. Vous pouvez également personnaliser le type hello de réponse qui sera renvoyé toouser lors de la demande est refusée. Par défaut, nous utilisons la réponse 403.

3. Cliquez maintenant sur l’onglet **Moteur de règles** sous **HTTP Large**. Vous utiliser cette fonctionnalité hello de tooapply onglet toodefine chemins d’accès, activer la fonctionnalité de l’authentification des jetons hello et activer l’authentification des jetons supplémentaire liées de fonctionnalités.

    - Utilisez toodefine élément multimédia de la colonne « IF » ou le chemin d’accès que vous souhaitez tooapply l’authentification des jetons. 
    - Cliquez sur tooadd « Jeton Auth » à partir de hello fonctionnalité déroulante tooenable jeton d’authentification.
        
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-token-auth/cdn-rules-engine-enable2.png)

4. Bonjour **moteur de règles** onglet, il existe quelques fonctionnalités supplémentaires, vous pouvez activer.
    
    - Code de refus d’authentification du jeton : détermine le type de hello de réponse qui sera renvoyé toouser lorsqu’une demande est refusée. Règles définies ici remplacent le paramètre de code hello refus dans l’onglet du jeton d’authentification hello.
    - Jeton auth ignorer : détermine si le jeton de toovalidate URL utilisée sera respecte la casse.
    - Paramètre de jeton d’authentification : renommer la requête de jeton d’authentification hello URL demandée de paramètre de chaîne indiquant hello. 
        
    ![Bouton de gestion du panneau de profil CDN](./media/cdn-token-auth/cdn-rules-engine2.png)

5. Vous pouvez personnaliser votre jeton, qui est une application qui génère un jeton pour les fonctionnalités d’authentification du jeton. Le code source est accessible dans [GitHub](https://github.com/VerizonDigital/ectoken).
Les langages disponibles sont notamment :
    
    - C
    - C#
    - PHP
    - Perl
    - Java
    - Python    


## <a name="azure-cdn-features-and-provider-pricing"></a>Tarification du fournisseur et des fonctionnalités du CDN Azure

Consultez hello [vue d’ensemble du CDN](cdn-overview.md) rubrique.
