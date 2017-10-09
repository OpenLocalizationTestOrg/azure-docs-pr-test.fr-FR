
Chaque point de terminaison possède un *port public* et un *port privé* :

* port public de Hello est utilisé par toolisten de programme d’équilibrage de charge Azure hello pour virtuels toohello du trafic entrant de hello Internet.
* un port privé Hello est utilisé par toolisten de machine virtuelle hello pour le trafic, généralement destination tooan application ou service qui s’exécute sur l’ordinateur virtuel de hello entrants.

Valeurs par défaut pour hello protocole IP et les ports TCP ou UDP pour les protocoles réseau connus sont fournis lorsque vous créez des points de terminaison avec hello portail Azure. Pour les points de terminaison personnalisés, vous devez toospecify hello correct protocole IP (TCP ou UDP) et les ports publics et privés hello. toodistribute du trafic entrant au hasard entre plusieurs machines virtuelles, vous devez toocreate un jeu d’équilibrage de charge composé de plusieurs points de terminaison.

Après avoir créé un point de terminaison, vous pouvez utiliser un règles contrôle d’accès (ACL) de liste toodefine qui donnent ou refusent le trafic entrant de hello toohello le port public du point de terminaison hello en fonction de son adresse IP de source. Toutefois, si l’ordinateur virtuel de hello est dans un réseau virtuel Azure, vous devez utiliser les groupes de sécurité réseau à la place. Pour plus d'informations, consultez [À propos des groupes de sécurité réseau](../articles/virtual-network/virtual-networks-nsg.md).

> [!NOTE]
> La configuration du pare-feu pour les machines virtuelles Azure s’effectue automatiquement pour les ports associés aux points de terminaison de connectivité à distance qu’Azure configure automatiquement. Pour les ports spécifiés pour tous les autres points de terminaison, aucune configuration ne s’effectue automatiquement le pare-feu de l’ordinateur virtuel de hello toohello. Lorsque vous créez un point de terminaison pour la machine virtuelle de hello, vous devez tooensure qui hello pare-feu d’ordinateur virtuel de hello autorise également le trafic de hello pour le protocole de hello et configuration de point de terminaison toohello port privé correspondante. tooconfigure hello pare-feu, consultez la documentation de hello ou de l’aide en ligne hello système d’exploitation en cours d’exécution sur l’ordinateur virtuel de hello.
>
>

## <a name="create-an-endpoint"></a>Création d’un point de terminaison
1. Si vous n’avez pas déjà fait, connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Cliquez sur **virtuels**, puis cliquez sur nom hello de machine virtuelle de hello que vous souhaitez tooconfigure.
3. Cliquez sur **points de terminaison** Bonjour **paramètres** groupe. Hello **points de terminaison** page répertorie tous les hello points de terminaison actuels pour la machine virtuelle de hello. (Cet exemple est une machine virtuelle Windows. Par défaut, une machine virtuelle Linux affiche un point de terminaison pour SSH.)

   <!-- ![Endpoints](./media/virtual-machines-common-classic-setup-endpoints/endpointswindows.png) -->
   ![Points de terminaison](./media/virtual-machines-common-classic-setup-endpoints/endpointsblade.png)

4. Dans la barre de commandes hello au-dessus des entrées de point de terminaison hello, cliquez sur **ajouter**.
5. Sur hello **ajouter le point de terminaison** , tapez un nom pour le point de terminaison hello dans **nom**.
6. Dans **Protocole**, choisissez **TCP** ou **UDP**.
7. Dans **Port Public**, tapez le numéro de port hello pour le trafic entrant à partir de hello Internet hello. Dans **Port privé**, tapez hello numéro de port sur le hello machine virtuelle écoute. Ces derniers peuvent être différents. Vérifiez que hello pare-feu sur l’ordinateur virtuel de hello a été configuré tooallow hello le trafic correspondant toohello protocol (étape 6) et le port privé.
10. Cliquez sur **OK**.

nouveau point de terminaison Hello s’afficheront sur hello **points de terminaison** page.

![Création du point de terminaison réussie](./media/virtual-machines-common-classic-setup-endpoints/endpointcreated.png)

## <a name="manage-hello-acl-on-an-endpoint"></a>Gérer hello ACL sur un point de terminaison
ensemble de hello toodefine d’ordinateurs qui peuvent envoyer le trafic, hello ACL sur un point de terminaison peut limiter le trafic basé sur l’adresse IP source. Suivez ces étapes tooadd, modifier ou supprimer une liste ACL sur un point de terminaison.

> [!NOTE]
> Si le point de terminaison hello fait partie d’un jeu d’équilibrage de charge, les modifications apportées toohello ACL sur un point de terminaison sont les points de terminaison tooall appliquée dans l’ensemble de hello.
>
>

Si l’ordinateur virtuel de hello est dans un réseau virtuel Azure, nous vous recommandons de groupes de sécurité réseau au lieu d’ACL. Pour plus d'informations, consultez [À propos des groupes de sécurité réseau](../articles/virtual-network/virtual-networks-nsg.md).

1. Si vous n’avez pas déjà fait, inscrivez-vous toohello portail Azure.
2. Cliquez sur **virtuels**, puis cliquez sur nom hello de machine virtuelle de hello que vous souhaitez tooconfigure.
3. Cliquez sur **Endpoints**. À partir de la liste de hello, sélectionnez le point de terminaison approprié hello. liste ACL de Hello est bas hello de page de hello.

   ![Spécifier les détails de l’ACL](./media/virtual-machines-common-classic-setup-endpoints/aclpreentry.png)

4. Utiliser des lignes de hello liste tooadd, supprimer ou modifier les règles pour une liste ACL et modifier leur ordre. Hello **sous-réseau distant** valeur est une plage d’adresses IP pour le trafic entrant en provenance d’Internet qui hello Azure charge équilibrage utilise toopermit ou refuser hello le trafic en fonction de son adresse IP de source de hello. Être vraiment toospecify hello plage d’adresses IP au format CIDR, également connu sous le format de préfixe adresse. Par exemple `10.1.0.0/8`.

 ![Nouvelle entrée ACL](./media/virtual-machines-common-classic-setup-endpoints/newaclentry.png)


Vous pouvez utiliser des règles tooallow uniquement le trafic à partir d’ordinateurs spécifiques correspondant tooyour des ordinateurs sur le trafic Internet ou toodeny hello à partir de plages d’adresses spécifiques et connus.

règles de Hello sont évaluées dans l’ordre, en commençant par la première règle de hello et se terminant par la règle du dernier hello. Cela signifie que les règles doivent être commandés auprès toomost moins restrictif restrictif. Pour plus d’informations et obtenir des exemples, consultez [Qu’est-ce qu’une liste de contrôle d’accès réseau ?](../articles/virtual-network/virtual-networks-acl.md).
