# 🐥 Rigor Poussin Miner 0% Fees

**Mineur GPU NVIDIA pour RIGOR — Minage SOLO haute performance**

Rigor Poussin Miner est un mineur GPU dédié à la blockchain **RIGOR**, utilisant l'algorithme `rgrpow01`.

Il permet de miner directement sur votre propre nœud RIGOR, sans passer par une pool, et de recevoir les récompenses des blocs trouvés sur votre portefeuille.

### ⚡ Caractéristiques

- **Minage SOLO** sur votre propre nœud RIGOR
- **GPU NVIDIA** : GTX 10xx, RTX 20xx, 30xx, 40xx et 50xx
- **Multi-GPU** : utilisation de plusieurs cartes simultanément
- **CUDA intégré** : aucune installation du toolkit CUDA nécessaire
- **Configuration simple** : adresse du portefeuille et lancement
- **Compatible Ubuntu 22.04+**

---

## 📥 1. Télécharger le mineur

Téléchargez la dernière version dans la section **Releases** du dépôt GitHub.

Ou utilisez les commandes suivantes en remplaçant les paramètres du dépôt :

```bash
wget https://github.com/Dorian-360/Rigor-poussin-miner/releases/download/v1.0.0/rigor-poussin-miner-linux-x86_64.tar.gz
tar -xzf rigor-poussin-miner-linux-x86_64.tar.gz
cd rigor-poussin-miner-linux-x86_64
```

## ⚙️ 2. Configurer le nœud RIGOR

Sur la machine hébergeant votre nœud RIGOR, configurez les accès RPC.

```bash
DIR=~/.rigor; mkdir -p "$DIR"; sed -i '/^rpcuser=/d;/^rpcpassword=/d;/^rpcbind=/d;/^rpcallowip=/d;/^server=/d' "$DIR/rigor.conf" 2>/dev/null; printf 'server=1\nrpcuser=user\nrpcpassword=monmotdepasse\nrpcbind=0.0.0.0\nrpcallowip=127.0.0.1\nrpcallowip=192.168.0.0/16\n' >> "$DIR/rigor.conf"
```

Si vous lancez le portefeuille officiel avec `./bin/rigord` ou `./bin/rigor-wallet`, remplacez `DIR=~/.rigor` par `DIR=<dossier-du-portefeuille>/data`.

Redémarrez ensuite le nœud :

```bash
rigor-cli stop
rigord -daemon
```

Attendez la synchronisation complète et la connexion à au moins un pair.

## 🚀 3. Démarrer le minage

**Nœud local :**

```bash
./rigor-poussin-miner --wallet rg1qVOTRE_ADRESSE
```

**Nœud distant sur votre réseau local :**

```bash
./rigor-poussin-miner --wallet rg1qVOTRE_ADRESSE --node http://192.168.1.50:8761
```

**Utiliser plusieurs GPU :**

```bash
./rigor-poussin-miner --wallet rg1qVOTRE_ADRESSE --gpu 0,1
```

Par défaut, tous les GPU compatibles sont utilisés.

## 🔄 4. Minage continu avec Screen

Pour maintenir le mineur actif et le redémarrer automatiquement en cas d'arrêt :

```bash
screen -dmS rigor bash -c 'while true; do ./rigor-poussin-miner --wallet rg1qVOTRE_ADRESSE; sleep 5; done'
```

Afficher le mineur :

```bash
screen -r rigor
```

Pour quitter l'affichage sans arrêter le minage : `Ctrl+A`, puis `D`.

## 🛠️ Options disponibles

| Option       | Description                            |
| ------------ | -------------------------------------- |
| `--wallet`   | Adresse RIGOR recevant les récompenses |
| `--node`     | Adresse RPC du nœud                    |
| `--gpu 0,1`  | Sélection des cartes graphiques        |
| `--rpc-user` | Identifiant RPC                        |
| `--rpc-pass` | Mot de passe RPC                       |

## 🔒 Sécurité

- Ne jamais exposer le port RPC `8761` directement sur Internet.
- Limiter les accès RPC aux adresses IP autorisées.
- Utiliser un mot de passe RPC fort.
- Ne jamais partager les clés privées de votre portefeuille.

## 📜 Licence

Distribué sous licence **GNU GPL v2**, conformément aux obligations applicables au code du mineur officiel RIGOR réutilisé.

---

**🐥 Rigor Poussin Miner — Powered by NVIDIA GPU**
