# TP2- Jeux de mots-Synthèse et analyse spectrale d’une gamme de musique
## Objectifs
- Comprendre comment manipuler un signal audio avec Matlab, en effectuant 
certaines opérations classiques sur un fichier audio d’une phrase enregistrée via 
un smartphone.
- Comprendre la notion des sons purs à travers la synthèse et l’analyse spectrale 
d’une gamme de musique.

>Commentaires : Il est à remarquer que ce TP traite en principe des signaux continus. 
Or, l'utilisation de Matlab suppose l'échantillonnage du signal. Il faudra donc être 
vigilant par rapport aux différences de traitement entre le temps continu et le temps 
discret.
>Tracé des figures : toutes les figures devront être tracées avec les axes et les 
légendes des axes appropriés.
>Travail demandé : un script Matlab commenté contenant le travail réalisé et des
commentaires sur ce que vous avez compris et pas compris, ou sur ce qui vous a 
semblé intéressant ou pas, bref tout commentaire pertinent sur le TP

« phrase.wave » est un fichier audio enregistré à l’aide d’un smartphone, en 
prononçant lentement la phrase : 
- « Rien ne sert de courir, il faut partir à point ». 
1. Sauvegardez ce fichier sur votre répertoire de travail, puis charger-le dans MATLAB 
à l’aide de la commande « audioread ».

``matlab
[x,f]= audioread("audioo.ogg"); 
``
2. Tracez le signal enregistré en fonction du temps, puis écoutez-le en utilisant la 
commande « sound ».
``matlab
sound(x,f) %audio original
``
3. Cette commande permet d’écouter la phrase à sa fréquence d’échantillonnage 
d’enregistrement. Ecoutez la phrase en modifiant la fréquence d’échantillonnage à 
double ou deux fois plus petite pour vous faire parler comme « Terminator » ou « 
Donald Duck ». En effet, modifier la fréquence d’échantillonnage revient à appliquer 
un changement d’échelle y(t) = x(at) en fonction de la valeur du facteur d’échelle, cela 
revient à opérer une compression ou une dilatation du spectre initial d’où la version 
plus grave ou plus aigüe du signal écouté.

```matlab
sound(x,f*0.5)  %audio dilaté
sound(x,f*3)  %audio compresse
```

4- Tracez le signal en fonction des indices du vecteur x, puis essayez de repérer les 
indices de début et de fin de la phrase « Rien ne sert de ».

```matlab
ts = 1/f; 
N = length(x); 
t = (0:N-1)*(10*ts); 
plot(t,x);
title('Rien ne sert de');
```
<img width="269" alt="tp2 4" src="https://user-images.githubusercontent.com/121026580/210187739-4e564b6e-443c-490e-85d5-14fa01cf1dac.png">

5. Pour segmenter le premier mot, il faut par exemple créer un vecteur « riennesertde »
contenant les n premières valeurs du signal enregistré x qui correspondent à ce 
morceau. Créez ce vecteur, puis écoutez le mot segmenté.
```matlab
rien_ne_sert_de = x(5150:23500);
sound(rien_ne_sert_de,f);
```
6. Segmentez cette fois-ci toute la phrase en créant les variables suivantes : 
riennesertde, courir, ilfaut, partirapoint.

```matlab
rien_ne_sert_de = x(5150:23500);
courir  = x(23500:31000);
il_faut = x(35000:43000);
partir_a_point  = x(45000:58000);
```
7. Notez que le signal initial de parole est un vecteur colonne contenant un certain 
nombre de valeurs (length(x)). Réarrangez ce vecteur pour écouter la phrase 
synthétisée « Rien ne sert de partir à point, il faut courir ».
```matlab
new_phrase =[rien_ne_sert_de,partir_a_point,il_faut,courir];
sound(new_phrase,f);
```
