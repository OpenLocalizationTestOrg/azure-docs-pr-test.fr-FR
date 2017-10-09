### <a name="gwipnoconnection"></a>adresse IP de passerelle dans toomodify hello réseau local - aucune connexion de passerelle

Utilisez hello exemple toomodify une passerelle de réseau local qui n’a pas d’une connexion de passerelle. Lorsque vous modifiez cette valeur, vous pouvez également modifier les préfixes d’adresse hello en hello même temps.

1. Sur hello des ressources de passerelle de réseau Local, Bonjour **paramètres** , cliquez sur **Configuration**.
2. Bonjour **adresse IP** zone, modifiez l’adresse IP de hello.
3. Cliquez sur **enregistrer** toosave les paramètres hello.

### <a name="gwipwithconnection"></a>toomodify hello local passerelle passerelle adresse IP de réseau - connexion de passerelle existante

toomodify une passerelle de réseau local qui dispose d’une connexion, vous devez supprimer la toofirst connexion hello. Une fois la connexion de hello est supprimée, vous pouvez modifier l’adresse IP de passerelle hello et recréez une nouvelle connexion. Vous pouvez également modifier les préfixes d’adresse hello en hello même temps. Cela entraînera une interruption de votre connexion VPN. Lorsque vous modifiez l’adresse IP de passerelle hello, vous n’avez pas besoin passerelle VPN de hello toodelete. Vous devez uniquement la connexion de hello tooremove.
 
#### <a name="1-remove-hello-connection"></a>1. Supprimer la connexion de hello.

1. Sur hello des ressources de passerelle de réseau Local, Bonjour **paramètres** , cliquez sur **connexions**.
2. Cliquez sur hello **...**  sur une ligne de hello pour la connexion de hello, puis cliquez sur **supprimer**.
3. Cliquez sur **enregistrer** toosave vos paramètres.

#### <a name="2-modify-hello-ip-address"></a>2. Modifier l’adresse IP de hello.

Vous pouvez également modifier les préfixes d’adresse hello en hello même temps.

1. Bonjour **adresse IP** zone, modifiez l’adresse IP de hello.
2. Cliquez sur **enregistrer** toosave les paramètres hello.

#### <a name="3-recreate-hello-connection"></a>3. Recréez la connexion de hello.

1. Accédez toohello passerelle de réseau virtuel pour votre réseau virtuel. (Pas hello passerelle de réseau Local.)
2. Sur hello passerelle de réseau virtuel, Bonjour **paramètres** , cliquez sur **connexions**.
3. Cliquez sur hello **+ ajouter** tooopen hello **ajouter une connexion** panneau.
4. Recréez votre connexion.
5. Cliquez sur **OK** connexion de hello toocreate.
