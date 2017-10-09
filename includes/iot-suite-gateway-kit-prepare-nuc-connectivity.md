## <a name="prepare-your-intel-nuc"></a>Préparer votre Intel NUC

le programme d’installation matérielle hello toocomplete, vous devez :

- Connectez l’alimentation Intel NUC toohello incluse dans le kit de hello.
- Connecter votre réseau de tooyour Intel NUC à l’aide d’un câble Ethernet.

Vous avez maintenant terminé la configuration du matériel de votre périphérique de passerelle Intel NUC hello.

### <a name="sign-in-and-access-hello-terminal"></a>Se connecter et accéder à Terminal Server de hello

Vous avez deux options tooaccess d’un environnement de Terminal Server sur votre NUC Intel :

- Si vous possédez un clavier et surveillez connecté tooyour Intel NUC, vous pouvez accéder directement à interpréteur de commandes hello. informations d’identification par défaut de Hello sont le nom d’utilisateur **racine** et le mot de passe **racine**.

- Interpréteur de commandes accès hello sur votre NUC Intel à l’aide de SSH à partir de votre ordinateur de bureau.

#### <a name="sign-in-with-ssh"></a>Se connecter avec SSH

toosign avec SSH, vous devez hello adresseIP de votre NUC Intel. Si vous possédez un clavier et surveillez connecté tooyour Intel NUC, utilisez hello `ifconfig` adresse IP de hello toofind de commandes. Vous pouvez également connecter tooyour routeur toolist hello des adresses de périphériques sur votre réseau.

Connectez-vous avec le nom d’utilisateur **root** et le mot de passe **root**.

#### <a name="optional-share-a-folder-on-your-intel-nuc"></a>Facultatif : partager un dossier sur votre Intel NUC

Si vous le souhaitez, vous souhaiterez tooshare un dossier sur votre NUC Intel avec votre environnement de bureau. Partage d’un dossier permet de vous toouse votre éditeur de texte de bureau par défaut (tel que [Visual Studio Code](https://code.visualstudio.com/) ou [texte Sublime](http://www.sublimetext.com/)) tooedit des fichiers sur votre NUC Intel au lieu d’utiliser `nano` ou `vi`.

tooshare un dossier avec Windows, configurer un serveur de Samba hello NUC d’Intel. Vous pouvez également utiliser hello SFTP sur hello Intel NUC avec un client SFTP sur votre ordinateur de bureau.
