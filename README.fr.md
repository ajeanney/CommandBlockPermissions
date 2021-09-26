# CommandBlockPermissions

Gardez les command blocks honnêtes : un joueur ne peut enregistrer une commande dans un command block que s'il a le droit de l'exécuter, personne ne contourne donc une permission en la branchant sur un bouton.

## Fonctionnement

Le plugin écoute les paquets `SET_COMMAND_BLOCK` et `SET_COMMAND_MINECART` avec ProtocolLib. Quand un joueur enregistre une commande, son nom est recherché dans la table des commandes du serveur :

- si la commande déclare une permission, le joueur doit l'avoir ;
- sinon, le joueur doit avoir `cbPerm.<commande>` ;
- si aucun des deux n'est vrai, le paquet est annulé et le joueur est prévenu, la commande n'atteint donc jamais le bloc.

Une commande vide est toujours autorisée, vider un command block étant inoffensif.

## Prérequis

- Spigot/Paper 1.17 ou supérieur.
- [ProtocolLib](https://github.com/dmulloy2/ProtocolLib), déclaré comme dépendance obligatoire.

## Installation

1. Déposez ProtocolLib et le jar compilé dans le dossier `plugins/` de votre serveur.
2. Redémarrez le serveur.

## Permissions

| Permission | Description |
| --- | --- |
| `cbPerm.<commande>` | Autorise le joueur à utiliser `<commande>` dans un command block, pour les commandes qui ne déclarent aucune permission |
| `cbPerm.*` | Autorise le joueur à utiliser n'importe quelle commande dans un command block |

Les commandes qui déclarent une permission continuent de l'utiliser : donnez au joueur la permission de la commande elle-même pour qu'il puisse la placer.

## Compilation

```sh
mvn clean package
```

Le jar shaded est écrit dans `target/`.
