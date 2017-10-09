## <a name="overview"></a>Vue d'ensemble

Dans ce didacticiel, vous effectuez hello comme suit :

- Déployer une instance de hello distant tooyour solution préconfigurée analyse abonnement Azure. Cette étape déploie et configure automatiquement plusieurs services Azure.
- Configurer votre toocommunicate de périphérique avec votre ordinateur et de la solution d’analyse à distance hello.
- Hello exemple périphérique code tooconnect toohello distant solution d’analyse de mise à jour et envoyer la télémétrie simulée que vous pouvez afficher sur le tableau de bord de solution hello.

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel, vous avez besoin d’un abonnement Azure actif.

> [!NOTE]
> Si vous ne possédez pas de compte, vous pouvez créer un compte d’évaluation gratuit en quelques minutes. Pour plus d’informations, consultez la rubrique [Version d’évaluation gratuite d’Azure][lnk-free-trial].

### <a name="required-software"></a>Logiciels requis

Vous devez client SSH sur votre tooenable d’ordinateur de bureau vous tooremotely accès hello de ligne de commande sur hello framboises Pi.

- Windows n’inclut pas de client SSH. Nous vous recommandons d’utiliser [PuTTY](http://www.putty.org/).
- La plupart des distributions Linux et Mac OS incluent l’utilitaire SSH hello. Pour plus d’informations, consultez [SSH Using Linux or Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md) (Utilisation de SSH avec Linux ou Mac OS).

### <a name="required-hardware"></a>Matériel requis

Un ordinateur de bureau de tooenable vous tooconnect à distance toohello de ligne de commande sur hello framboises Pi.

[Starter Kit Microsoft IoT pour Raspberry Pi 3][lnk-starter-kits] ou composants équivalents. Ce didacticiel utilise les éléments suivants à partir du kit de hello de hello :

- Raspberry Pi 3
- Carte MicroSD (avec NOOBS)
- Un câble mini USB
- Un câble Ethernet

[lnk-starter-kits]: https://azure.microsoft.com/develop/iot/starter-kits/
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/