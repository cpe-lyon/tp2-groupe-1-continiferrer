# Compte-Rendu TP2 / Contini E. Ferrer H. / Groupe 5

RDV sur [CPE e-campus](https://prod.e-campus.cpe.fr/pluginfile.php/36441/mod_resource/content/0/TP2.pdf) pour obtenir le TP

## Exercice 1 - Variables d’environnement
1. Bash trouve les commandes de l'utilisateur dans les dossiers renseignés dans la variable **PATH** 
```bash
$ printenv PATH
# /usr/local/sbin:/usr/local/bin: ...
```
2. C'est la variable **HOME**
```bash
$ printenv HOME
# /home/server
```
3. RÔLE DES **VARIABLES**
```bash
$ printenv LANG # détermine la langue
$ printenv PWD # contient le chemin vers le working directory
$ printenv OLDPWD # contient le chemin absolu vers le previous working directory
$ printenv SHELL # contient le chemin vers /bin/bash
$ printenv _ # contient le chemin du binaire de printenv
```
4. Création d'une variable
```bash
$ MY_VAR="ZOZO" # [export] une pour variable globale
$ printenv MY_VAR
```
5. La commande bash
```bash
$ bash # Lance bash
$ echo $MY_VAR # Ne retourne rien, car on se place dans un nouvel environnement hérité du bash père (on ne conserve donc pas les variables locales)
```
6. cf. question 4
7. Question 7
```bash
$ export NOMS="Enzo Hugo"
$ printenv NOMS
```
8. Commande qui dit bonjour en utilisant **NOMS**
```bash
$ echo "Bonjour à vous deux, $NOMS !"
```
9. différence entre unset et variable à valeur vide
```bash
$ unset NOMS # Variable NOMS n'existe plus
$ NOMS="" # Tout simplement pas de contenu, la variable existe
``` 
10. Utilisation de la commande **echo** pour écrire :
```bash
echo \$HOME = $HOME # affiche : $HOME = /home/server
```
## Exercice 2 - Contrôle de mot de passe
- Création du fichier **testpwd**.**sh** dans le dossier scripts
```bash
$ mkdir scripts
$ cd scripts
$ touch testpwd.sh
$ nano testpwd.sh
```
- Dans nano :
```bash
#!/bin/bash
motDePasse="toto"
mdp=""
read -s "Saisissez votre mot de passe : " mdp
if [ "$mdp" = "$motDePasse" ]; then
    echo -e "\nt'es trop fort Guy, that's it !"
else
    echo -e "\nLe mot de passe de correspond pas Guy."
fi
```
## Exercice 3 - Expressions rationnelles
```bash
#!/bin/bash
function is_number(){
    re='^[+-]?[0-9]+([.][0-9]+)?$'
    if ! [[ $1 =~ $re ]] ; then
        return 1
    else
        return 0
    fi
}
is_number $1
if [ $? = 0 ] ; then
    echo "EH Guy ! it's not a real number"
else
    echo "Guy t'es trop fort !"                                                                                                                         
```
## Exercice 4 - Contrôle d’utilisateur
```bash
#!/bin/bash
if [ -z $1 ]; then
    echo -e "C'est vide Guy !\nTry again like a boss: ./user.sh <user>"
elif cut -f5 -d ':' /etc/passwd | grep -w -q $1; then
    echo "Cet utilisateur existe, t'es chaud !"
else
    echo "Tu t'es trompé Guy, ce mec n'existe pas !"
fi
``` 
## Exercice 5 - Factorielle
```bash
#!/bin/bash
function factorielle()
{
    if [ $1 -eq 0 ]; then
        echo 1;
    elif [ $1 -lt 0 ]; then
        echo "Votre nombre doit être au moins égal à 0"
    else
        echo $(( $1 * `factorielle $(( $1 - 1 ))` ))
    fi
}
```
## Exercice 6 - Le juste prix

## Exercice 7 - Statistiques

## Exercice 8 - Pour les plus rapides

## TIPS

- Pour afficher au fur et à mesure un man (par exemple) : **man --help | more**
- Un **chemin absolu** commence par un **/**
