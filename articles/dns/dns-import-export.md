---
title: "aaaImport et une zone de domaine d’exportation du fichier tooAzure DNS à l’aide d’Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment tooimport et exporter un serveur DNS de la zone fichier tooAzure DNS à l’aide d’Azure CLI 1.0"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a>Importer et exporter un fichier de zone DNS à l’aide de hello Azure CLI 1.0 

Cet article vous guide tout au long de la tooimport et exportation de fichiers de zone DNS pour Azure DNS à l’aide de hello Azure CLI 1.0.

## <a name="introduction-toodns-zone-migration"></a>Migration de zone de présentation tooDNS

Un fichier de zone DNS est un fichier texte qui contient les détails de chaque enregistrement de nom de domaine (DNS) dans la zone de hello. Il suit un format standard, ce qui permet le transfert d’enregistrements DNS entre différents systèmes DNS. À l’aide d’un fichier de zone est rapide, fiable et pratique tootransfer une zone DNS dans ou hors d’Azure DNS.

DNS Azure prend en charge l’importation et exportation des fichiers de zone à l’aide de hello Azure interface de ligne de commande (CLI). Importation de fichier de zone est **pas** actuellement pris en charge via Azure PowerShell ou hello portail Azure.

Bonjour Azure CLI 1.0 est un outil de ligne de commande multiplateforme utilisé pour la gestion des services Azure. Il est disponible pour les plateformes Windows, Mac et Linux de hello de hello [page Téléchargements Azure](https://azure.microsoft.com/downloads/). Prise en charge multiplateforme est important pour l’importation et exportation de fichiers de zone, étant donné que hello courants logiciel de serveur de nom, [lier](https://www.isc.org/downloads/bind/), s’exécute généralement sur Linux.

> [!NOTE]
> Il existe actuellement deux versions de hello CLI d’Azure. CLI1.0 est basé sur Node.js et offre des commandes commençant par « azure ».
> CLI2.0 est basé sur Python et offre des commandes commençant par « az ». Importation de fichier de zone est pris en charge dans les deux versions, nous vous recommandons l’utilisation des commandes CLI1.0 hello, comme décrit dans cette page.

## <a name="obtain-your-existing-dns-zone-file"></a>Comment obtenir votre fichier de zone DNS existant

Avant d’importer un fichier de zone DNS dans le système DNS Azure, vous devez tooobtain une copie du fichier de zone hello. source de Hello de ce fichier dépend de la zone DNS de hello actuellement héberge.

* Si votre zone DNS est hébergé par un service partenaire (par exemple, un bureau d’enregistrement de domaine, dédié fournisseur d’hébergement DNS ou fournisseur de cloud autre), ce service doit fournir le fichier de zone DNS hello capacité toodownload hello.
* Si votre zone DNS est hébergé sur le DNS de Windows, le dossier par défaut de hello pour les fichiers de zone hello est **%systemroot%\system32\dns**. fichier de zone tooeach Hello chemin d’accès complet s’affiche également sur hello **général** onglet de la console DNS de hello.
* Si votre zone DNS est hébergé à l’aide de BIND, emplacement hello hello du fichier de zone pour chaque zone est spécifié dans le fichier de configuration de liaison hello **named.conf**.

> [!NOTE]
> Le format des fichiers de zone téléchargés à partir de GoDaddy diffère légèrement du format standard. Vous avez besoin toocorrect cela avant d’importer ces fichiers de zone DNS Azure.
>
> Les noms DNS Bonjour RDATA de chaque enregistrement DNS sont spécifiés en tant que noms complets, mais ils n’ont pas une fin «. » Cela signifie qu’ils sont interprétés comme des noms relatifs par d’autres systèmes DNS. Vous devez terminer hello tooappend tooedit hello zone fichier «. » tootheir noms avant de les importer dans Azure DNS.
>
> Par exemple, hello l’enregistrement CNAME « www 3600 CNAME contoso.com » doit être modifié trop « contoso.com IN CNAME de www 3600. »
> (avec un «. » final).

## <a name="import-a-dns-zone-file-into-azure-dns"></a>Importation d’un fichier de zone DNS dans Azure DNS

L’importation d’un fichier de zone crée une nouvelle zone dans Azure DNS si celle-ci n’existe pas. Si la zone de hello existe déjà, hello jeux d’enregistrements dans le fichier de zone hello doit être fusionnés avec les jeux d’enregistrements existants hello.

### <a name="merge-behavior"></a>Comportement de la fusion

* Par défaut, les nouveaux jeux d’enregistrements sont fusionnés avec les jeux d’enregistrements existants. Les enregistrements identiques dans un jeu d’enregistrements fusionné sont dédupliqués.
* Vous pouvez également, en spécifiant hello `--force` option, hello remplace de processus d’importation des jeux d’enregistrements existants avec les nouveaux jeux d’enregistrements. Jeux d’enregistrements existants qui n’ont pas un enregistrement correspondant défini dans le fichier de zone importé hello ne sont pas supprimés.
* Lors de la fusion de jeux d’enregistrements, hello toolive TTL (time) préexistants de jeux d’enregistrements est utilisé. Lorsque `--force` est utilisé, hello durée de vie d’un nouvel ensemble d’enregistrements hello est utilisé.
* Début de paramètres d’autorité principale (SOA) (à l’exception de `host`) sont toujours effectuées à partir du fichier de zone importé hello, indépendamment du fait que `--force` est utilisé. De même, pour hello enregistrement de serveur de noms défini au sommet de zone hello, hello TTL toujours provient du fichier de zone importé hello.
* Un enregistrement CNAME importé ne remplace pas un enregistrement CNAME existant enregistre par hello même nom, sauf si hello `--force` paramètre est spécifié.
* Lorsqu’un conflit se produit entre un enregistrement CNAME et un autre enregistrement de même nom, mais il est différent de hello tapez (indépendamment de ce qui est existant ou nouveau), enregistrement de hello existant est conservé. Cette valeur est indépendante d’utilisation hello de `--force`.

### <a name="additional-information-about-importing"></a>Informations supplémentaires sur l’importation

Hello remarques suivantes fournissent des informations techniques sur fuseau de hello processus d’importation.

* Hello `$TTL` la directive est facultative et il est pris en charge. Lorsqu’aucun `$TTL` la directive est fournie, l’importation des enregistrements sans une durée de vie explicite définir la valeur par défaut de tooa durée de vie de 3 600 secondes. Lorsque deux enregistre dans le même jeu d’enregistrements hello spécifier TTLs différents, une valeur inférieure hello est utilisée.
* Hello `$ORIGIN` la directive est facultative et il est pris en charge. Lorsqu’aucun `$ORIGIN` est définie par défaut de hello valeur utilisée est le nom de la zone hello tel que spécifié sur la ligne de commande hello (ainsi que la fin d’exécution hello «. »).
* Hello `$INCLUDE` et `$GENERATE` directives ne sont pas pris en charge.
* Les types d’enregistrements A, AAAA, CNAME, MX, NS, SOA, SRV et TXT sont pris en charge.
* Hello enregistrement SOA est créé automatiquement par le système DNS Azure lors de la création d’une zone. Lorsque vous importez un fichier de zone, tous les paramètres SOA proviennent du fichier de zone hello *sauf* hello `host` paramètre. Ce paramètre utilise la valeur hello fournie par le système DNS Azure. Il s’agit, car ce paramètre doit désigner le serveur de noms principal toohello fournie par le système DNS Azure.
* Hello nom serveur jeu d’enregistrements au sommet de zone hello sont également créé automatiquement par le système DNS Azure lors de la zone de hello est créée. Uniquement hello durée de vie de ce jeu d’enregistrements est importée. Ces enregistrements contiennent des noms de serveur de nom hello fournies par le système DNS Azure. données d’enregistrement de Hello ne sont pas remplacées par valeurs hello contenues dans le fichier de zone importé hello.
* Pour la version préliminaire publique, Azure DNS prend uniquement en charge les enregistrements à chaîne unique. Chaîne multiple enregistrements TXT sont être concaténées et tronquée too255 caractères.

### <a name="cli-format-and-values"></a>Format et valeurs de l’interface CLI

format Hello tooimport de commande CLI d’Azure hello une zone DNS est :

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

Valeurs :

* `<resource group>`est le nom hello hello du groupe de ressources pour la zone DNS Azure hello.
* `<zone name>`est le nom hello de zone de hello.
* `<zone file name>`est le nom de chemin/hello de toobe de fichier de zone hello importé.

Si une zone portant ce nom n’existe pas dans le groupe de ressources hello, il est créé pour vous. Si hello zone existe déjà, hello jeux d’enregistrements importés est fusionnés avec les jeux d’enregistrements existants. toooverwrite hello existant jeux d’enregistrements, utilisez hello `--force` option.

format de hello tooverify d’un fichier de zone sans réellement son importation, utilisez hello `--parse-only` option.

### <a name="step-1-import-a-zone-file"></a>Étape 1. Importer un fichier de zone

tooimport un fichier de zone de hello **contoso.com**.

1. Se connecter tooyour abonnement Azure à l’aide de hello Azure CLI 1.0.

    ```azurecli
    azure login
    ```

2. Sélectionnez l’abonnement hello où vous souhaitez toocreate votre nouvelle zone DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. Azure DNS étant un service Gestionnaire de ressources uniquement Azure, hello CLI d’Azure doit être en mode de gestionnaire de tooResource commuté.

    ```azurecli
    azure config mode arm
    ```

4. Avant d’utiliser service DNS Azure de hello, vous devez inscrire votre fournisseur de ressources abonnement toouse hello Microsoft.Network. (Cette opération n’est à effectuer qu’une fois pour chaque abonnement.)

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. Si vous n’avez pas déjà, vous devez également toocreate un groupe de ressources du Gestionnaire de ressources.

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. zone de hello tooimport **contoso.com** à partir du fichier de hello **contoso.com.txt** dans une zone DNS dans le groupe de ressources hello **myresourcegroup**, exécutez la commande de hello `azure network dns zone import`.<BR>Cette commande charge le fichier de zone hello et l’analyser. commande Hello exécute une série de commandes sur fuseau de hello Azure DNS service toocreate hello et tous les enregistrements de hello définit dans la zone de hello. commande Hello signale la progression dans la fenêtre de console hello, ainsi que les erreurs ou avertissements. Étant donné que les jeux d’enregistrements est créés dans la série, il peut prendre quelques minutes tooimport un fichier de zone volumineux.

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a>Étape 2. Vérifiez que la zone de hello

tooverify hello zone DNS après avoir importé le fichier de hello, vous pouvez utiliser l’une des méthodes suivantes de hello :

* Vous pouvez répertorier les enregistrements hello à l’aide de hello suivant commande CLI d’Azure :

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* Vous pouvez répertorier les enregistrements hello en utilisant l’applet de commande PowerShell hello `Get-AzureRmDnsRecordSet`.
* Vous pouvez utiliser `nslookup` tooverify résolution de noms pour les enregistrements de hello. Zone de hello n’est pas déléguées encore, vous devez explicitement toospecify hello correct Azure serveurs DNS. Hello exemple suivant montre comment les noms de serveur de nom tooretrieve hello assignés toohello zone. INFORMATIQUE montre également comment enregistre des tooquery hello « www » à l’aide de `nslookup`.

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a>Étape 3. Mettre à jour la délégation DNS

Après avoir vérifié que zone de hello a été importé correctement, vous devez tooupdate hello DNS délégation toopoint toohello Azure serveurs de noms DNS. Pour plus d’informations, voir l’article hello [mettre à jour la délégation DNS hello](dns-domain-delegation.md).

## <a name="export-a-dns-zone-file-from-azure-dns"></a>Exportation d’un fichier de zone DNS à partir d’Azure DNS

format Hello tooimport de commande CLI d’Azure hello une zone DNS est :

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

Valeurs :

* `<resource group>`est le nom hello hello du groupe de ressources pour la zone DNS Azure hello.
* `<zone name>`est le nom hello de zone de hello.
* `<zone file name>`est le nom de chemin/hello de toobe de fichier de zone hello exportée.

Comme avec l’importation de zone hello, vous devez d’abord toosign dans, choisissez votre abonnement et configurer le mode de gestionnaire de ressources toouse hello CLI d’Azure.

### <a name="tooexport-a-zone-file"></a>tooexport un fichier de zone

1. Se connecter tooyour abonnement Azure à l’aide de hello CLI d’Azure.

    ```azurecli
    azure login
    ```

2. Sélectionnez l’abonnement hello où vous souhaitez toocreate votre zone DNS.

    ```azurecli
    azure account set <subscription name>
    ```

3. Azure DNS est un service Azure Resource Manager uniquement. Hello CLI d’Azure doit être en mode de gestionnaire de tooResource commuté.

    ```azurecli
    azure config mode arm
    ```

4. tooexport hello zone DNS Azure existante **contoso.com** dans le groupe de ressources **myresourcegroup** toohello fichier **contoso.com.txt** (dans le dossier actif hello), exécutez `azure network dns zone export`. Cette commande appelle hello tooenumerate du service DNS Azure jeux d’enregistrements dans la zone de hello et exporter le fichier de zone hello résultats tooa liaison compatible.

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
