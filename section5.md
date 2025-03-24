---

exports:
  - format: pdf
    template: plain_latex
    output: ./exports/section5.pdf
downloads:
  - file: ./exports/section5.pdf
    title: PDF
title: Section 5 - Supports de transmission
abstract: |
  Section 5 aborde les phénomènes liés à la distorsion et au canal de transmission. Tout d'abord, elle traite de la distorsion, distinguant clairement la distorsion dans les systèmes linéaires de la distorsion non linéaire. Ensuite, la section examine le canal de transmission en introduisant la limite de Shannon, une frontière théorique définissant la capacité maximale de transmission sans erreurs pour un canal donné. Des exemples pratiques de modèles physiques de canaux sont également présentés pour illustrer ces concepts théoriques. Par la suite, la section détaille le modèle statistique du canal, essentiel à l'analyse de performance des systèmes de communication. Elle présente notamment le modèle de canal binaire, largement utilisé pour quantifier les performances d'un canal en termes de taux d'erreur binaire. L'objectif **O5** est ainsi de comprendre et d'analyser les différentes formes de distorsion ainsi que les caractéristiques des canaux de transmission afin de pouvoir évaluer leur impact sur les performances des systèmes de communication et mettre en place les solutions adaptées pour minimiser les erreurs.
   

---

 


## Supports de transmission

Un **canal de transmission** est le support permettant la transmission d’un signal entre un émetteur et un récepteur dans un système de communication. Ce canal peut être un médium physique, tel qu’un câble ou une fibre optique, ou encore un médium sans fil comme l’air ou l’espace. Quelle que soit sa nature, le canal influence le signal transmis en introduisant divers phénomènes perturbateurs, tels que du bruit, des interférences et de la distorsion.



:::{important} Exemples pratiques
La **paire torsadée** est un canal constitué de deux fils conducteurs enroulés ensemble, conçu pour réduire les interférences électromagnétiques et utilisé principalement pour des signaux à basses fréquences (quelques centaines de kHz).

```{figure} images/sec5-ch1.png
:label: sec5-ch1.png
:align: center 
Structure simplifiée d'une paire torsadée, canal adapté aux fréquences de quelques centaines de kHz.
``` 


Le **câble coaxial** est formé d'un conducteur central entouré de plusieurs couches isolantes et d'une gaine métallique protectrice. Ce type de canal permet de transporter des signaux sur une large bande passante (jusqu’à plusieurs centaines de MHz), offrant une protection contre les interférences externes.

```{figure} images/sec5-ch2.png
:label: sec5-ch2.png
:align: center 
Schéma d'un câble coaxial montrant le conducteur central et les gaines isolantes, avec une bande passante atteignant des centaines de MHz.
``` 

La **fibre optique** utilise la lumière pour transporter des informations. Un convertisseur électro-optique transforme le signal électrique en impulsions lumineuses qui traversent une fibre en verre. À l’autre extrémité, ces impulsions lumineuses sont reconverties en signal électrique grâce à un capteur optique, permettant ainsi une transmission à très haut débit et sur de longues distances.

```{figure} images/sec5-ch3.png
:label: sec5-ch3.png
:align: center 
Principe de fonctionnement d'une fibre optique : conversion électrique-optique et transmission de la lumière dans une fibre de verre. 
``` 

Enfin, la **liaison sans fil** (*wireless link*) transmet les signaux dans l'air ou le vide à l’aide d’antennes. Le signal d’information est modulé sur une onde porteuse à haute fréquence, ce qui permet de transmettre les données sans support physique direct. Ce type de transmission est largement utilisé pour la radio, la télévision, la téléphonie mobile et les communications par satellite.

```{figure} images/sec5-ch4.png
:label: sec5-ch4.png
:align: center 
 Illustration d'une liaison sans fil avec modulation d'une onde porteuse émise et reçue par antenne. (Les antennes sont fréquemment représentées par des triangles inversés)
``` 
:::




###   Distorsion




Les effets du canal (distortion) peuvent être regroupés en deux catégories principales : les effets linéaires et non linéaires. La **distortion linéaire** inclue l’atténuation, où la puissance du signal diminue avec la distance ou la nature du canal, la dispersion, provoquant l'étalement du signal dans le temps ou en fréquence, et la propagation par trajets multiples (multi-trajet), générant des interférences dues à la réflexion et à la diffraction des ondes. Ces phénomènes sont généralement modélisables par des équations linéaires et traités par des outils mathématiques comme la convolution ou l'analyse fréquentielle (donc les effets linéairessont modélisés comme un système linéaire, en utilisant une réponse impulsionnelle (ou une réponse fréquentielle)). 

En revanche, la **distortion non linéaire** provient d'une relation non proportionnelle entre l’entrée et la sortie du canal, souvent causée par les composants électroniques tels que les amplificateurs. Ces effets ne peuvent pas simplement être modélisés comme un filtre ; la sortie doit donc être caractérisée en fonction de la réponse du système à chaque entrée spécifique. Parmi ces effets figurent les distorsions harmoniques et d’intermodulation, qui créent des fréquences parasites indésirables et plus complexes à gérer. 

L'objectif principal de l'introduction de modèles mathématiques est de quantifier précisément les effets du canal sur les ressources du système de communication, notamment la puissance du signal et la bande passante disponible. Grâce à ces modèles, il devient possible d'optimiser les ressources, d'améliorer la robustesse des systèmes de communication face aux imperfections du canal, et de déterminer les limites théoriques de performance comme définies par la capacité de Shannon.



#### Distorsion linéaire

Nous présentons ici un modèle mathématique décrivant la distorsion linéaire.  Le signal de message $m(t)$ est d'abord modulé sur une onde porteuse, donnant naissance au signal transmis $x(t)$. Ce dernier traverse ensuite un canal caractérisé par une réponse impulsionnelle $h(t)$ (ou sa réponse fréquentielle associée $H(f)$). À la sortie du canal, le signal reçu $y(t)$ subit l'ajout d'un bruit thermique $b(t)$, générant ainsi le signal perturbé $r(t)$ avant sa démodulation.


```{figure} images/sec5-distlin.png
:label: sec5-distlin.png
:align: center 
 Schéma d'une transmission linéaire avec modulation, caractérisant l'effet du canal par sa réponse impulsionnelle et l'ajout d'un bruit thermique. 
``` 
 

Nous pouvons chercher à identifier l'impact de la distorsion à l'aide des **harmoniques**. Un harmonique désigne une composante fréquentielle d'un signal périodique, dont la fréquence est un multiple entier de la fréquence fondamentale du signal initial. Par exemple, si un signal possède une fréquence fondamentale (ou première harmonique), les harmoniques suivantes (2ème, 3ème, 4ème, etc.) auront des fréquences égales à deux, trois, quatre fois ou plus cette fréquence fondamentale.

Dans un signal complexe, les harmoniques jouent un rôle essentiel dans la forme finale du signal. La manière dont les harmoniques s'additionnent influence fortement la forme d'onde résultante. Ainsi, si l’amplitude d’un harmonique augmente significativement, ou si sa phase se décale, le signal total peut subir des modifications notables, entraînant une distorsion non linéaire. Par conséquent, le contrôle précis des amplitudes et des phases des harmoniques est crucial pour préserver l’intégrité du signal transmis dans les systèmes de communication.


```{figure} images/sec5-distlin-amp.png
:label: sec5-distlin-amp.png
:align: center 
  Illustration de la distorsion non linéaire par modification de l'amplitude des harmoniques. 
``` 
 

 ```{figure} images/sec5-distlin-ph.png
:label: sec5-distlin-ph.png
:align: center 
  Illustration de la distorsion non linéaire par modification de la phase des harmoniques. 
``` 
 








####   Distorsion non linéaire

La distorsion harmonique aussi apparaît  lorsqu'un signal traverse un système non linéaire, où la réponse du système n’est pas directement proportionnelle à l'entrée.


 ```{figure} images/sec5-sysnon.png
:label: sec5-sysnon.png
:align: center 
   Représentation simplifiée d’un système non linéaire caractérisé par une relation entrée-sortie. 
``` 



En pratique, l'analyse de la distorsion harmonique se fait en considérant spécifiquement la réponse du système pour chaque entrée donnée. Cela signifie que la forme et l’amplitude des harmoniques générées dépendent directement à la fois des caractéristiques intrinsèques du système étudié (sa réponse non linéaire) et de la nature exacte du signal d’entrée. Par conséquent, il est essentiel d’effectuer cette analyse au cas par cas, pour déterminer précisément comment la combinaison système-entrée affecte la qualité et l'intégrité du signal transmis.


 ```{figure} images/sec5-nonlin.png
:label: sec5-nonlin.png
:align: center 
   Illustration graphique de la distorsion harmonique générée par la réponse non linéaire d'un système à un signal sinusoïdal en entrée. Un signal sinusoïdal appliqué à l'entrée subit une déformation lorsqu'il traverse le système, en raison de la relation non linéaire entre l'entrée et la sortie. La courbe représentant cette relation (caractéristique du système non linéaire) montre clairement une déviation par rapport à la linéarité. Ainsi, le signal obtenu à la sortie est modifié, présentant une forme d'onde différente de celle du signal d'entrée initial, caractéristique de la distorsion harmonique.
``` 
 









:::{note} Exemple illustratif : Distorsion harmonique 
La **distorsion harmonique** désigne un phénomène non linéaire caractérisé par l'apparition d'harmoniques. Cette distorsion résulte d'un comportement non proportionnel du système entre l'entrée et la sortie, altérant ainsi la forme originale du signal transmis et potentiellement affectant sa qualité et sa fidélité.

Soit un système caractérisé par une relation entrée-sortie polynomiale exprimée par :
$$
y(t) = \alpha x(t) + \beta x^2(t) + \gamma x^3(t)
$$

Lorsque le signal d’entrée considéré est un signal sinusoïdal simple de la forme :
$$
x(t) = A \cos(2\pi f_0 t)
$$

la sortie obtenue après passage dans le système présente des composantes supplémentaires par rapport à l'entrée initiale. En effet, en développant les termes de sortie selon les puissances du signal d'entrée, on obtient explicitement :
$$
y(t) = \frac{\beta A^2}{2} + \left(\alpha A + \frac{3\gamma A^3}{4}\right)\cos(2\pi f_0 t) + \frac{\beta A^2}{2}\cos(4\pi f_0 t) + \frac{\gamma A^3}{4}\cos(6\pi f_0 t)
$$

Cette expression révèle clairement la présence de nouvelles fréquences (les « harmoniques »), qui sont des multiples entiers de la fréquence fondamentale $f_0$. Plus précisément, en plus de la fréquence fondamentale $f_0$, apparaissent désormais les fréquences $2f_0$ et $3f_0$. Ces fréquences additionnelles génèrent ce qu’on appelle la distorsion harmonique, typique d’un comportement non linéaire du système.

:::

:::{note} Exemple illustratif : Distorsion d’intermodulation 

La **distorsion d'intermodulation** est  le phénomène par lequel un système non linéaire génère des composantes fréquentielles supplémentaires résultant de combinaisons additives ou soustractives des fréquences initiales des signaux appliqués à son entrée.

Considérons un système non linéaire caractérisé par une relation entrée-sortie de deuxième ordre :
$$
y(t) = \alpha x(t) + \beta x^2(t)
$$

Lorsque deux signaux sinusoïdaux distincts sont appliqués à l'entrée, de la forme :
$$
x(t) = A_1\cos(2\pi f_1 t) + A_2\cos(2\pi f_2 t)
$$
le signal de sortie obtenu après développement mathématique est donné par :

$$
y(t) = \frac{\beta A_1^2}{2} + \frac{\beta A_2^2}{2} + \alpha A_1\cos(2\pi f_1 t) + \alpha A_2\cos(2\pi f_2 t) 
+ \frac{\beta A_1^2}{2}\cos(4\pi f_1 t) + \frac{\beta A_2^2}{2}\cos(4\pi f_2 t)
+ \beta A_1 A_2 \cos[2\pi(f_1 - f_2)t] 
+ \beta A_1 A_2 \cos[2\pi(f_1 + f_2)t]
$$

On observe ainsi l’apparition de nouvelles fréquences : les harmoniques des signaux d’entrée ($2f_1$ et $2f_2$) et les combinaisons fréquentielles ($f_1 + f_2$ et $f_1 - f_2$). Ces nouvelles composantes issues de la combinaison des fréquences fondamentales sont caractéristiques de la distorsion d'intermodulation.
:::

### Canal de transmission


La transmission d’un signal numérique à travers un canal est modélisé comme un filtre passe-bas. Le signal numérique, caractérisé par un débit de bits $R_b = \frac{1}{T_b}$ bits par seconde, traverse le canal ayant une bande passante disponible de $B$ Hz. À la sortie du canal, le signal reçu $y(t)$ est perturbé par un bruit thermique $b(t)$, ce qui génère le signal résultant $r(t)$ envoyé au démodulateur.

La capacité maximale du canal (en bits par seconde) est donnée par la célèbre formule de Claude Shannon :
$$
C = B \log_2\left(1 + \frac{\overline{x^2(t)}}{\overline{b^2(t)}}\right)
$$

Cette formule exprime la capacité maximale théorique (débit maximal sans erreurs possible) d'un canal de bande passante $B$ Hz, en fonction du rapport signal à bruit (SNR), représenté par le rapport entre la puissance moyenne du signal, $\overline{x^2(t)}$, et la puissance moyenne du bruit, $\overline{b^2(t)}$. En pratique, cette équation indique que pour augmenter la capacité, il est possible d’accroître la bande passante disponible ou d'améliorer le rapport signal à bruit, c’est-à-dire en augmentant la puissance du signal ou en réduisant le niveau de bruit. La capacité calculée par cette formule est une limite théorique fondamentale, non dépassable, quel que soit le codage utilisé.



 ```{figure} images/sec5-Shannon.png
:label: sec5-Shannon.png
:align: center 
   Transmission numérique à travers un canal bruité et limite théorique de capacité selon la formule de Shannon.
``` 
 





###  Modèle statistique du canal
Un modèle simplifié de **canal binaire**, est utilisé pour étudier la transmission d'une information binaire ($\texttt{0}$ ou $\texttt{1}$) à travers un canal de communication potentiellement bruité. Dans ce modèle, l’information émise (notée \( E \)) peut prendre deux valeurs possibles : $\texttt{0}$ ou $\texttt{1}$. La décision prise à la réception (notée \( D \)) peut également être $\texttt{0}$ ou $\texttt{1}$.


 ```{figure} images/sec5-BSC.png
:label: sec5-BSC.png
:align: center 
   Modèle statistique d’un canal binaire présentant les probabilités de décisions correctes et erronées.  
``` 



Les paramètres représentés sont les probabilités conditionnelles :
- $\text{Pr}(D=\texttt{1}|E=\texttt{1})$ : Probabilité que la décision soit correcte ($\texttt{1}$ reçu sachant que $\texttt{1}$ a été envoyé).
- $\text{Pr}(D=\texttt{0}|E=\texttt{0})$ : Probabilité que la décision soit correcte ($\texttt{0}$ reçu sachant que $\texttt{0}$ a été envoyé).
- $\text{Pr}(D=\texttt{0}|E=\texttt{1})$: Probabilité d'erreur, décidant $\texttt{0}$ alors que $\texttt{1}$ était envoyé.
- $\text{Pr}(D=\texttt{1}|E=\texttt{0} )$ : Probabilité d'erreur, décidant $\texttt{1}$ alors que $\texttt{0}$ était envoyé.

Les relations suivantes sont vérifiées :
$$
\text{Pr}(D=\texttt{0}|E=\texttt{1}) + \text{Pr}(D=\texttt{1}|E=\texttt{1}) = 1
$$
$$
\text{Pr}(D=\texttt{0}|E=\texttt{0}) + \text{Pr}(D=\texttt{1}|E=\texttt{0}) = 1
$$

Ces probabilités permettent de caractériser précisément la performance du canal en termes de fiabilité et de taux d'erreur binaire.
 
 
 La **probabilité d'erreur moyenne** pour un canal binaire décrit la probabilité qu'un bit transmis soit incorrectement reçu. Elle est définie par :La probabilité d'erreur moyenne pour un canal binaire décrit la probabilité qu'un bit transmis soit incorrectement reçu. Elle est définie par :
$$
\text{Pr(Erreur)} = \text{Pr}(D=\texttt{0}, E=\texttt{1}) + \text{Pr}(D=\texttt{1}, E=\texttt{0})
$$

En développant cette expression à l'aide des probabilités conditionnelles, on obtient :
$$
\text{Pr(Erreur)} = \text{Pr}(D=\texttt{0}|E=\texttt{1})\text{Pr}(E=\texttt{1}) + \text{Pr}(D=\texttt{1}|E=\texttt{0})\text{Pr}(E=\texttt{0})
$$

:::{warning}  Le taux d'erreur moyen d'un canal binaire symétrique

Dans le cas spécifique où les bits $\texttt{0}$ et $\texttt{1}$ sont équiprobables, c'est-à-dire lorsque :
$$
\text{Pr}(E=\texttt{1}) = \text{Pr}(E=\texttt{0}) = \frac{1}{2}
$$
la probabilité d'erreur moyenne se simplifie en :
$$
\text{Pr(Erreur)} = \frac{\text{Pr}(D=\texttt{0}|E=\texttt{1}) + \text{Pr}(D=\texttt{1}|E=\texttt{0})}{2}
$$
:::
 

 ## Resumé

Cette section traite de  **O5.**  *Modélisation d'un canal de transmission et explication des  imperfections associées*.  Elle explore les différents supports de transmission, incluant les canaux physiques (paire torsadée, câble coaxial, fibre optique) et sans fil, ainsi que les effets des canaux tels que la distorsion linéaire (atténuation, dispersion, trajets multiples) et non linéaire (distorsions harmonique et d'intermodulation). Un accent particulier est mis sur les modèles mathématiques permettant de caractériser ces effets, notamment à travers l'analyse fréquentielle et l'étude des harmoniques. La formule de Shannon est introduite pour illustrer la limite théorique de capacité d'un canal, soulignant l'importance du rapport signal-bruit et de la bande passante disponible.

 