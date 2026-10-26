# rigor-poussin-miner

Mineur GPU NVIDIA pour **RIGOR** (algorithme rgrpow01), en minage SOLO sur votre propre nœud.
Ubuntu 22.04 et plus récent, toutes les cartes NVIDIA depuis les GTX 10xx (pilote NVIDIA requis, pas besoin de CUDA).

## 1. Configurer le nœud (une seule fois)

Sur la machine où tourne le nœud RIGOR, collez :

```bash
DIR=~/.rigor; mkdir -p $DIR; sed -i '/^rpcuser=/d;/^rpcpassword=/d;/^rpcbind=/d;/^rpcallowip=/d;/^server=/d' $DIR/rigor.conf 2>/dev/null; printf 'server=1\nrpcuser=user\nrpcpassword=monmotdepasse\nrpcbind=0.0.0.0\nrpcallowip=127.0.0.1\nrpcallowip=192.168.0.0/16\n' >> $DIR/rigor.conf
```

> Si vous lancez le portefeuille officiel avec `./bin/rigord` ou `./bin/rigor-wallet`, remplacez `DIR=~/.rigor` par `DIR=<dossier-du-portefeuille>/data`.

Puis **redémarrez le nœud** :

```bash
rigor-cli stop     # ou fermez complètement le portefeuille
rigord -daemon     # ou relancez le portefeuille
```

Attendez que le nœud soit synchronisé et ait au moins un pair.

## 2. Télécharger le mineur

```bash
wget https://github.com/VOTRE_COMPTE/VOTRE_DEPOT/releases/latest/download/rigor-poussin-miner-linux-x86_64.tar.gz
tar xzf rigor-poussin-miner-linux-x86_64.tar.gz
cd rigor-poussin-miner-linux-x86_64
```

## 3. Lancer

Nœud sur la même machine :

```bash
./rigor-poussin-miner --wallet rg1qVOTRE_ADRESSE
```

Nœud sur une autre machine du réseau :

```bash
./rigor-poussin-miner --wallet rg1qVOTRE_ADRESSE --node http://192.168.1.50:8761
```

Avec redémarrage automatique dans screen :

```bash
screen -dmS rigor bash -c 'while true; do ./rigor-poussin-miner --wallet rg1qVOTRE_ADRESSE; sleep 5; done'
screen -r rigor    # voir le mineur (Ctrl-A puis D pour détacher)
```

## Options utiles

| Option | Rôle |
|---|---|
| `--wallet rg1q...` | adresse de paiement (obligatoire) |
| `--node http://IP:8761` | nœud distant (défaut : 127.0.0.1) |
| `--gpu 0,1` | choisir les GPU (défaut : tous) |
| `--rpc-user` / `--rpc-pass` | autres identifiants que `user` / `monmotdepasse` |

## Sécurité

Les identifiants par défaut sont publics. Ne publiez **jamais** le port 8761 sur Internet et gardez `rpcallowip` limité à votre réseau local. Vous pouvez changer le mot de passe dans `rigor.conf` et utiliser `--rpc-pass` côté mineur.

## Licence

GPL v2 : le mineur contient du code du mineur officiel RIGOR.
