---

exports:
  - format: pdf
    template: plain_latex
    output: ./exports/section3.pdf
downloads:
  - file: ./exports/section3.pdf
    title: PDF
title: Section 3 - Numérisation 
abstract: |
 Cette section explore les bases de la numérisation des signaux, une étape clé dans les systèmes de communication modernes. Elle introduit tout d’abord les principes fondamentaux de l’échantillonnage, qui permettent de convertir un signal continu en une série d’échantillons discrets, garantissant ainsi une représentation fidèle selon le théorème de Nyquist-Shannon. Les applications pratiques de l’échantillonnage, notamment le calcul du débit maximal d’information et les modulations analogiques d’impulsions, y sont abordées. Ensuite, la section s’intéresse à la modulation par impulsions codées (*Pulse Code Modulation*; PCM), un processus crucial pour la transmission numérique des signaux. Les concepts de codage et de quantification sont détaillés pour expliquer comment les niveaux d’amplitude sont discrétisés en valeurs numériques. Enfin, la section conclut par une étude du multiplexage temporel, une technique permettant de partager efficacement un canal de communication entre plusieurs utilisateurs. Les principes de base et le format des trames sont explorés pour illustrer son importance dans les systèmes à grande échelle.

---

 


## Numérisation

La **numérisation** implique la transformation d'un signal du temps continu au temps discret (échantillonnage), puis en valeurs discrètes (quantification).  La numérisation est réalisée par un **convertisseur analogique-numérique** (*analog-to-digital converter*; ADC).
Sa performance  généralement indiquée par la fréquence d’échantillonnage et le nombre de bits par échantillon.
Le processus inverse, qui consiste à convertir un signal numérique en un signal continu, est effectué par un **convertisseur numérique-analogique** (*digital-to-analog converter*, DAC). 

```{figure} images/overview.png
:label: Overview-DAC
:align: center
Schéma du processus de numérisation et de reconstruction d’un signal. Le signal analogique de message est d’abord converti en signal numérique via une conversion analogique-numérique (A/N), qui comprend l’échantillonnage à une période $T_E $ et la quantification définie par $ \Delta, N, Q(\cdot) $. Le signal numérisé est ensuite reconverti en signal analogique par une conversion numérique-analogique (N/A), où une interpolation est appliquée à l’aide de la fonction $p(t)$ pour reconstruire une approximation du signal d’origine.
```


### Échantillonnage (*Sampling*)

(def-chantillonnage)=
Définition: Échantillonnage  
: L’**échantillonnage** est la lecture d’un signal, $m(t)$ à intervalles réguliers, $T_E$ seconds ($T_E$ est la période d’échantillonnage). Donc on utilise une fréquence d'échantionnage de $f_E$ Hz. La problématique principale liée à l’échantillonnage **sans perdre d’information**.  Cela nous permet d'utiliser l'interpolation et de reconstituer le signal original. Nous représenterons le signal échantillonné comme $m_E(t)$.

```{figure} images/sampling.png
:label: sampling
:align: center
 Schéma du processus d’échantillonnage d’un signal. Le signal analogique $m(t)$ est multiplié par un **train d’impulsions** $ \delta_{T_E}(t) $, représentant une suite de deltas de Dirac espacés de $T_E$. Cette opération produit le signal échantillonné $ m_E(t) $, qui conserve les valeurs de $m(t)$ aux instants d’échantillonnage. Ce processus est la première étape de la conversion analogique-numérique (A/N), garantissant une représentati on discrète du signal original.
```



Soit $m(t)$ un signal limité (dans le domaine des fréquences) à $B$ Hz. Le signal échantillonné est :
$$
m_E(t) = m(t) \delta_{T_E}(t) = \sum_{n=-\infty}^{\infty} m(nT_E) \delta(t - nT_E)
$$
où $\delta_{T_E}(t)$ représente un train d'impulsions de Dirac, défini comme [](#train), et  $m(nT_E)$ représente la valeur de $m(t)$ à $t = nT_E$ sec. Sachant que 
$$
\delta_{T_E}(t) = \sum_{n=-\infty}^{\infty} \delta (t - nT_E) = \frac{1}{T_E} \sum_{n=-\infty}^{\infty} e^{j 2\pi n f_E t}
$$
la transformée de Fourier de $g_E(t)$ peut être écrite comme 
$$
M_E(f) = M(f) * \frac{1}{T_E} \sum_{n=-\infty}^{\infty} \delta(f - n f_E) = \frac{1}{T_E} \sum_{n=-\infty}^{\infty} M(f - n f_E)
$$


```{figure} images/sampling-before.png
:label: sampling-before
:align: center
Un exemple de signal de message à bande limitée, $B$ Hz.
```


```{figure} images/sampling-after.png
:label: sampling-after
:align: center
La version échantillonnée du signal dans le domaine fréquentiel devient périodique avec une fréquence  $f_E $, qui est la fréquence d'échantillonnage. **Remarque :** Tant que $f_E > 2B $, il n’y a pas de recouvrement (aliasing). Les copies peuvent rester non chevauchantes.
```


:::{warning} Attention
Notez que le spectre du signal d’origine devient périodique après échantillonnage avec une période de $f_E =\frac{1}{T_E}$.
:::

### Reconstruction  



Selon le **théorème d'échantillonnage de Nyquist-Shannon**, un signal, $m(t)$ dont le spectre est limité à une bande de fréquences comprise entre $ -B $ et $ B $ Hz peut être parfaitement reconstruit à partir de ses échantillons **si et seulement si** la fréquence d’échantillonnage $ f_E $ respecte la condition 
$$
f_E \geq 2B
$$
Le **taux de Nyquist** ($ 2B $) est définie comme la fréquence minimale d'échantillonnage nécessaire pour éviter le **chevauchement** lors de la numérisation d'un signal. Donc le taux de Nyquist représente donc la **fréquence d'échantillonnage minimale requise** pour assurer une reconstruction fidèle du signal sans perte d’information.


 
(def-chantillonnage)=
Définition: chevauchement (*aliasing*) 
: Nous devons nous conformer aux critères de Nquist, sinon nous observons un effet de **chevauchement**.   Le chevauchement se produit lorsqu'un signal est échantillonné à une fréquence **inférieure** au **taux de Nyquist** ($f_E < 2B$). Ce chevauchement entraîne une **distorsion irréversible** du signal, où différentes fréquences deviennent indiscernables.

:::{warning} Attention
Comment éviter le chevauchement :
1. **Augmenter la fréquence d’échantillonnage** pour que $f_E > 2B$. Mais notez que échantillonnage au-dessus du taux de Nyquist réduira l'efficacité spectrale (certaines bandes ne sont pas utilisées).


2. **Appliquer un anti-chevauchment** avant l’échantillonnage pour éliminer les composantes fréquentielles supérieures à $B$ (i.e. pour limiter la largeur de bande de $g(t)$.
:::
 


#### Reconstruction idéale

Si un signal $ m(t) $ a été échantillonné avec une fréquence $ f_E \geq 2B $, la reconstruction idéale est réalisée en **filtrant le spectre du signal échantillonné** avec un **filtre passe-bas idéal** dont la réponse en fréquence est :
$$
H(f) = T_E \cdot \prod \left( \frac{f}{2B} \right) = \begin{cases} 
T_E & \text{si } |f| \leq B \\
0 & \text{si } |f| > B \end{cases} 
$$
où $ \prod(x) $ représente une fonction porte qui sélectionne uniquement les fréquences comprises entre $ -B $ et $ B $ Hz. Ce filtre passe-bas idéal élimine les copies spectrales indésirables introduites lors de l’échantillonnage.

En domain temporel, $m(t)$ peut être parfaitement reconstruit par **interpolation de sinc** :
$$
m(t) = \sum_{n=-\infty}^{\infty} m(nT_E) \text{sinc} \left(   \frac{\pi(t - nT_E)}{T_E} \right)
$$


%- $ \text{sinc}(\pi x) = \frac{\sin(\pi x)}{\pi x} $ est la fonction de cardinal de Whittaker-Shannon utilisée pour l’interpolation.
 

 ```{figure} images/reconstuctruction-ideal.png
:label: reconstuctruction-ideal
:align: center
Un **filtre passe-bas idéal** est utilisé pour extraire la bande originale de largeur $2B$, éliminant ainsi les répliques spectrales et permettant la reconstruction du signal initial.
```


#### Reconstruction pratique (interpolation) 


L’**interpolation** est le processus de reconstruction d'un signal continu à partir de ses échantillons discrets en utilisant un **filtre passe-bas** ayant une réponse impulsionnelle $p(t)$.


```{figure} images/reconstuction-pratique.png
:label: reconstuction-pratique
:align: center
Modèle équivalent de reconstruction d’un signal échantillonné. Le signal échantillonné $ m_E(t)$est filtré par un **filtre passe-bas** ayant une réponse impulsionnelle $ p(t) $ et une réponse en fréquence $ P(f) $. Ce filtrage permet d’éliminer les répliques spectrales indésirables et de reconstruire une approximation du signal original, notée $ \tilde{m}(t) $. Cette approche constitue une **reconstruction pratique** du signal après l’étape d’échantillonnage.
```


Lorsque nous ne pouvons pas créer un filtre idéal, nous pouvons utiliser un filtre pratique avec une réponse impulsionnelle p(t)p(t) qui a une durée finie dans le temps, permettant une reconstruction approximative tout en réduisant la complexité de mise en œuvre. L'interpolation peut être vue comme un filtrage de convolution du signal échantillonné $m_E(t)$ avec un **filtre passe-bas non-idéal** avec une  **réponse impulsionnelle** du filtre passe-bas $ p(t) $, qui permet de lisser les échantillons et de reconstruire un signal continu :
$$
 \widetilde{m}(t) = m_E(t) * p(t) = \sum_{n=-\infty}^{\infty} m(nT_E) p(t - nT_E)
$$
où $\widetilde{m}(t)$ est le **signal reconstruit** et  $*$ représente l’opération de **convolution**.



L'expression de la transformée de Fourier du signal reconstruit est donnée par :
$$
\widetilde{M}(f) = M_E(f) P(f) = P(f) \frac{1}{T_E} \sum_{n=-\infty}^{\infty} M(f - n f_E)
$$
où  $\tilde{G}(f) $ est le spectre du **signal reconstruit**, $ M_E(f)$ est le spectre du **signal échantillonné**, et  $ P(f)$ est la **réponse en fréquence du filtre d’interpolation** $ p(t)$. 



:::{warning}  Comment peut-on éliminer l'effet de $ p(t)$ ?
L'effet de $ p(t)$ peut être éliminé en appliquant un **égaliseur** (*equalizer*). L’égaliseur est l’équivalent d’un filtre passe bas ayant une fonction de transfert inverse  (ou annule $ p(t)$).   
Soit \( E(f) \) la **réponse en fréquence de l'égaliseur**. Notre objectif de conception est d'obtenir 
$$
E(f) P(f) =
\begin{cases} 
0, & |f| \geq f_E - B \\
T_E e^{-j 2\pi f t_0}, & |f| < B
\end{cases}
$$
où $\textcolor{red}{t_0}$ est un délai qui assure la causalité du filtre conçu. Notez que nous nous concentrons uniquement sur la largeur de bande du message. 


 ```{figure} images/equalization.png
:label: equalization
:align: center
Schéma du processus d’égalisation appliqué au signal reconstruit. Le signal $ \tilde{m}(t) $, obtenu après interpolation, est traité par un **égaliseur** ayant une réponse impulsionnelle $ e(t) $ et une réponse en fréquence $ E(f) $. L’objectif de ce filtrage est de compenser les distorsions introduites par le processus de transmission et de reconstruction, produisant ainsi un signal égalisé $\bar{ \bar{m}}(t) $, plus fidèle au signal d'origine.
```
:::


 


 

### Quantification (*Quantization*)


(def-quantification)=
Définition: Quantification
: La **quantification** est la lecture d'un signal analogique avec une précision finie. Une conséquence importante de ce processus est l'ajout du  bruit de quantification. La quantification est utilisée après l'échantillonnage dans le processus de numérisation d'un signal.  Nous représenterons le signal après la quantification comme $m_E(t)$ 


La quantification est un système  qui transforme un signal d’entrée analogique  à temps continu  en un signal de sortie numérique à temps continu, en l'arrondissant à l’un des niveaux prédéfinis. Elle peut être représentée par une fonction de quantification
$$
y = Q(x)
$$

:::{note} Exemple  illustratif :  
- Nombre de niveaux de quantification : \( 2^3 = 8 \)
- Marge de fonctionnement : de -4V à +4V
- Pas de quantification (\(\Delta\)) : 
$$
  \Delta = \frac{\text{plage de quantification}}{\text{nombre de niveaux}} = \frac{4 - (-4)}{8} = \frac{8}{8} = 1V
  $$
  Ainsi, chaque niveau est espacé de 1V.

 
Le signal est quantifié aux valeurs suivantes :
- Entrée \([-4V, -3.5V]\) → Quantifié à **-3.5V**
- Entrée \([-3.5V, -2.5V]\) → Quantifié à **-2.5V**
- Entrée \([-2.5V, -1.5V]\) → Quantifié à **-1.5V**
- Entrée \([-1.5V, -0.5V]\) → Quantifié à **-0.5V**
- Entrée \([-0.5V, +0.5V]\) → Quantifié à **+0.5V**
- Entrée \([+0.5V, +1.5V]\) → Quantifié à **+1.5V**
- Entrée \([+1.5V, +2.5V]\) → Quantifié à **+2.5V**
- Entrée \([+2.5V, +3.5V]\) → Quantifié à **+3.5V**

Toute valeur comprise dans un intervalle est arrondie au niveau de quantification le plus proche. Ce processus entraîne une **erreur de quantification**, qui dépend directement du pas de quantification $\Delta$.
 ```{figure} images/quantification-ex.png
:label: quantification-ex
:align: center
Illustration du processus de quantification utilisant **3 bits**, générant $2^3 = 8$ niveaux de quantification dans une plage de **-4V à +4V**. L'intervalle de quantification est $\Delta = 1V$.   Chaque valeur d’entrée $ m(nT_s) $ est arrondie au niveau de quantification le plus proche, produisant le signal quantifié $ \widetilde{m}(nT_s) $. Cette quantification entraîne une **erreur de quantification**, qui dépend du pas de quantification $\Delta = 1V $.

```
:::



 



#### Bruit de Quantification 
Soit **nombre total de niveaux disponibles**  représenté  par $L$ par une fonction $y=Q(x)$. On a besoin de $N$ bits pour chaque échantillon  où 
$$
L = 2^N
$$
Le **bruit de quantification** est l'erreur introduite après la quantification. Cette erreur est due à l’arrondi des valeurs du signal à l’un des niveaux de quantification disponibles.

L’échantillon quantifié est donné par :
$$
\hat{m}(nT_E) = m(nT_E) + q(nT_E)
$$
où $ m(nT_E) $ est le signal de message (signal d'origine) et $ q(nT_E) $ est le bruit de quantification ajouté.

La PDF du bruit $ q(nT_E) $ est **uniforme**, et  
$$
-\frac{\Delta}{2} \leq q(nT_s) < \frac{\Delta}{2}
$$
avec 
$$
\Delta = \frac{2m_p}{L}
$$
où en général  $-m_p \leq m(t) \leq m_p$. 


Le bruit de quantification est centré en moyenne et sa valeur moyenne est
$$
m_Q = E[q(nT_E)] = 0,  
$$
et sa variance est
$$
\quad \sigma_Q^2 = \frac{m_p^2}{3L^2}
$$


```{figure} images/quantification-model.png
:label: quantification-model
:align: center
L'erreur est ajoutée au signal discrétisé, ce qui donne le signal quantifié $ \hat{m}(nT_E)$, utilisé pour la transmission ou le traitement numérique. La quantification introduit une **distorsion**, dont l'impact dépend du pas de quantification $ \Delta $ et du nombre de bits utilisés $N$.
```


 
Le **rapport signal sur bruit de quantification** (*signal-to-quantization-noise ratio*; SQNR) est une mesure de la qualité du signal après quantification. Il est défini par :
$$
SQNR = \frac{ \textrm{Puissance de } m(T_E)}{\textrm{Puissance de }  q(nT_E)} = 3L^2 \frac{m^2(t)}{m_p^2}
$$

Le bruit de quantification est un facteur critique dans la conversion analogique-numérique, et il doit être minimisé pour assurer une haute fidélité du signal converti. Notez qu'un nombre de niveaux de quantification $L$ plus élevé réduit le bruit de quantification, mais mous avons besoin de plus de bits  pour représenter les échantillons ($N \times \textrm{le nombre total d'échantillons}$). 

#### Types de fonctions de quantification
Il existe deux types de fonctions de quantification.
- **Quantification Uniforme** :     Lorsque les niveaux de quantification sont **équidistants**, on parle de **quantification uniforme**. L'intervalle entre chaque niveau est appelé **pas de quantification** (*quantization step*) $ \Delta $ .

-  **Quantification Non Uniforme** :      Utilisée lorsque certaines plages de valeurs doivent être plus précises (ex : **compandage en télécommunications**).

 ```{figure} images/quantification-comparison.png
:label: quantification-comparison
:align: center
Exemples pour deux types de fonctions de quantification. Dans la quantification uniforme (à gauche), les niveaux sont répartis de manière égale sur toute la plage de signal, tandis que dans la quantification non uniforme (à droite), les niveaux sont plus denses pour les faibles amplitudes, réduisant ainsi l’erreur de quantification pour les signaux de faible intensité. Cette approche est couramment utilisée pour améliorer le rapport signal/bruit dans les systèmes de communication.
```


### Applications: Modulations analogiques d’impulsions  



La **modulation analogique d’impulsions** est une technique utilisée pour transmettre un **signal analogique** en modulant une série d’impulsions discrètes. Cette technique est largement employée en télécommunications et en traitement du signal. On utilise un signa de message qui porte l’information, $m(t)$ et une série d’impulsions (*pulses*) est utilisée pour moduler le signal, $p(t)$. La serie d’impulsions est est représentée par
$$
\sum_{n=-\infty}^{\infty} p(t - nT_E)
$$
où $p(t)$ est la **forme de l’impulsion** utilisée. 

 ```{figure} images/applications-def.png
:label: applications-def
:align: center
Illustration du processus d’échantillonnage à l’aide d’un train d’impulsions $p(t).  
```


Ces impulsions serviront à coder le signal en utilisant différentes méthodes de modulation telles que :
  - **PAM (Pulse Amplitude Modulation)** : Modulation en amplitude des impulsions. L'amplitude des impulsions change. 
  - **PWM (Pulse Width Modulation)** : Modulation de durée. La position des impulsions est la même, leur durée change.

  - **PPM (Pulse Position Modulation)** : Modulation en position des impulsions. La durée des impulsions est la même, leur position change.
  


```{figure} images/applications-type.png
:label: applications-type
:align: center
Une illustration de la PAM, PWM et PPM. (Voir: Exemples Intéractifs: Numérisation)
```


## Modulation par impulsions codées (*Pulse Code Modulation*; PCM)


Modulation par impulsions codées (PCM) est un système pratique d'échantillonnage et de quantification.

 
La **modulation par impulsions codées (PCM - Pulse Code Modulation)** est une technique de numérisation utilisée pour convertir un **signal analogique** en un **signal numérique**. Elle se déroule en trois étapes principales :
1. **Échantillonnage** : Le signal analogique est prélevé à intervalles réguliers.
2. **Quantification** : Chaque échantillon est arrondi à l’un des $  L $  iveaux disponibles.
3. **Codage en ligne** (*line coding*): Les niveaux quantifiés sont convertis en **mots binaires**.

 
  ```{figure} images/PCM.png
:label: PCM
:align: center
Schéma du processus de modulation par codage d'impulsions (PCM). Le signal analogique est d'abord échantillonné avec une période  $T_E$, puis quantifié en utilisant $ \Delta, N, Q(\cdot) $. Ensuite, un codage de ligne est appliqué à la séquence numérique via une fonction de codage $ p(t)$, influençant l’efficacité spectrale $ \eta_{\text{spectrale-binaire}} $. En sortie, un signal modulé en bande de base (autour de $0$ Hz)  est obtenu, caractérisé par un débit binaire $ R_b$ et une largeur de bande $B_T $.

```
La quantification est une étape essentielle du système **PCM**, où chaque échantillon $ m(nT_E) $ du signal $ m(t) $  est **approximé** par l’un des $ L $  niveaux de quantification et  
$$
  \Delta = \frac{2m_p}{L}
  $$ 
  
:::{note} Exemple  illustratif :    
  le nombre total de niveaux est :
$$
L = 8
$$
et le nombre de bits nécessaires pour coder chaque échantillon est :
$$
N = \log_2(L) = \log_2(8) = 3 \text{ bits}.
$$
 ```{figure} images/PCM-ex.png
:label: PCM-ex
:align: center

```




:::

À la sortie du système PCM, nous avons un **signal binaire** caractérisé par deux **paramètres de conception** :
- $ R_b $ : **Débit binaire**,  en bits/sec.
- $ B_T $ : **Largeur  de bande requise**,  en Hz.
 
Les paramètres $R_b $ et $ B_T$ sont influencés par la  forme d’impulsion $p(t)$  utilisée pour coder les bits. Différents schémas de codage binaire, comme **NRZ (Non-Return to Zero) ou Manchester** (*line coding*), affectent l’efficacité spectrale du signal transmis. 

Pour concevoir le système de communication, on doit definir l’**efficacité spectrale binaire** 
$$
\eta_{\text{spectrale-binaire}} = \frac{R_b}{B_T} \quad \text{bits/sec/Hz}
$$
Elle exprime **le nombre de bits transmis par seconde et par Hz de bande passante**.


D’après le **théorème de Nyquist**, l’efficacité spectrale maximale pour un signal binaire sans interférence intersymbole (*inter symbol interference*; ISI) est :
$$
\eta_{\text{spectrale-binaire}} \leq 2 \text{ bits/sec/Hz}
$$

Cela signifie que, dans un **canal idéal**, un débit binaire maximum de $2B_T$ bits/sec peut être atteint en utilisant des **impulsions optimales**.



#### Largeur de Bande de Transmission - PCM Binaire

Pour un **PCM binaire**, chaque échantillon est quantifié en utilisant $L$ niveaux de quantification, chaque échantillon est codé sur $N$ bits.  Si le signal analogique $ m(t)$ est **limité en fréquence** à $ B $ Hz, **le théorème de Nyquist** impose un minimum de $ 2B $ échantillons/sec pour une reconstruction parfaite.  Comme chaque échantillon est représenté par $ N $bits, le **débit binaire total** est :
  $$
  R_b = 2NB \quad \text{bits/sec}
  $$
et donc la **largeur de bande minimale** nécessaire pour la transmission de la sortie de PCM est :
  $$
  B_{T,\min} = \frac{R_b}{\eta_{\text{spectrale-binaire, max}}} = NB \quad \text{Hz}
  $$
[Lahti&Ding 5e édition:  Équation 5.37, page 312]. 






:::{warning} Attention
L’**efficacité spectrale** est un facteur clé dans la conception des systèmes de transmission numérique. Elle permet d’optimiser le **debit de transmission** tout en minimisant l’**utilisation de la largeur de bande**. Plus le nombre de bits $ N$ est élevé, plus la  largeur de bande $B_T$ nécessaire pour la transmission du signal est importante.
 :::





##  Multiplexage temporel (*Time Division Multiplexing*)

 
(def-TDM)=
Définition: Multiplexage temporel 
: Le **multiplexage temporel** (*Time Division Multiplexing*; TDM) est une technique permettant de **combiner plusieurs signaux utilisateurs** en un seul flux (*flow*) de transmission en allouant des intervalles de temps distincts à chaque signal.

:::{important} Exemple pratique : Système T1 de BELL
Le **système T1**, utilisé en télécommunications, applique le multiplexage temporel pour transmettre plusieurs canaux vocaux sur une seule ligne. Les principales étapes sont : 
1. Échantillonnage des canaux (pour chaqe utilisateur)
   - 24 canaux vocaux sont échantillonnés **en séquence** à un taux de 8 kHz.
2. Multiplexage PAM  
   - Après échantillonnage, la sortie représente un signal PAM où chaque échantillon est multiplexé par répartition temporelle.
3. Quantification et codage (*line coding*)
   - Chaque échantillon est quantifié et converti en un mot de 8 bits par un convertisseur analogique-numérique (ADC). La sortie est  une séquence binaire.
4. Transmission du signal numérique 
   - Le signal numérisé et multiplexé est ensuite transmis sur une ligne dédiée.


Le calcul pour le débit binaire total du système T1 : 
- Nombre de canaux : $ 24 $
- Fréquence d’échantillonnage par canal :$ f_E = 8 $ kHz
- Nombre de bits par échantillon : $ N = 8 $

Le **débit binaire total** $ R_b $ est donné par :
$$
R_b = \text{Nombre de canaux} \times \text{Fréquence d’échantillonnage} \times \text{Bits par échantillon}
$$
$$
R_b = 24 \times 8 \times 10^3 \times 8 = 1.536 \text{ Mbps}
$$
::: 


### Format de la Trame  

(def-Frame)=
Définition: Trame
:  Une **trame** (*frame*) est un segment contenant un **mot de code (échantillon)** pour chacun des  canaux dans un système.


:::{important} Exemple pratique : Structure de la Trame dans un Système T1
Dans un **système T1**, l’organisation des données suit ces étapes :

1. Chaque canal est échantillonné et converti en un **mot de code** de **8 bits**.
2. Une trame contient **un mot de code pour chaque canal**.
3. La structure de la trame est donc :
   $$
   24 \times 8 = 192 \text{ bits}
   $$
   Ainsi, une trame transporte 192 bits d’information.


Le **taux de trame** est de :
$$
8000 \text{ trames/sec}
$$
Cela correspond à la *fréquence d’échantillonnage* des signaux audio téléphoniques de 8 kHz.


Chaque trame a une durée de :
$$
T_{\text{trame}} = \frac{1}{8000} = 125 \ \mu s
$$
Chaque canal vocal est échantillonné à 8 kHz, donc un nouvel échantillon est pris toutes les 125 µs. Le système doit donc transmettre une trame complète chaque 125 µspour garantir la synchronisation et la qualité du signal.
:::


 ```{figure} images/TDM.png
:label: TDM
:align: center
Un exemple de multiplexage temporel (TDM) avec deux utilisateurs. Si chaque utilisateur transmet à un débit de $ R_b $ bits/seconde, alors la trame TDM doit être transmise à un débit de $ 2R_b$  bits/seconde. Cela est nécessaire pour préserver l'intégrité des données de chaque utilisateur et garantir que toutes les informations sont transmises sans perte.
```



 Dans un système de TDM (comme le  T1), les données sont transmises en  trames successives. Pour que le récepteur puisse identifier correctement les données et éviter tout décalage, il doit connaître la position de chaque trame.
Pour cette raison, un **bit de cadrage** (*framing bit*) est ajouté au début de chaque trame. Ce  bit permettre au récepteur de détecter le début de chaque trame. Donc il sert de repère temporel et assure la  synchronisation  entre l’émetteur et le récepteur.

:::{important} Exemple pratique : Taille totale de la trame avec bit de cadrage
Avec ce bit supplémentaire, la taille totale de la trame devient :

$$
192 \text{ bits} + 1 \text{ bit de cadrage} = 193 \text{ bits par trame}
$$

 ```{figure} images/Trame-T1.png
:label: Trame-T1
:align: center
Une illustration d'une trame T1.
```



:::


## Resumé

Cette section traite de **O3** *Numérisation des signaux : Comprendre l’échantillonnage, la quantification, et les conversions analogique-numérique*, qui concerne la numérisation des signaux, englobant l’échantillonnage, la quantification et les conversions analogique-numérique. La numérisation repose sur plusieurs paramètres influençant la qualité et l’efficacité de la transmission. L’échantillonnage est caractérisé par sa fréquence $f_E$, qui doit être au moins égale à $2B$ pour éviter l’aliasing, conformément au théorème de Nyquist, ainsi que par la période d’échantillonnage $T_E = \frac{1}{f_E}$. La quantification implique l’approximation de chaque échantillon à un niveau discret parmi $L$ niveaux possibles, où le nombre de bits par échantillon est déterminé par $n = \log_2 L$, générant un bruit de quantification . La PCM convertit ces échantillons en séquences binaires, définissant un débit binaire $R_b = 2nB$, qui détermine la bande passante requise $B_T = \frac{R_b}{\eta_{\text{spectrale}}}$, avec une limite maximale de $2$ bits/sec/Hz selon Nyquist. Le multiplexage temporel (TDM) regroupe les canaux des utilisateurs dans une trame unique, comprenant des bits de cadrage essentiel pour assurer la synchronisation entre l’émetteur et le récepteur. Une conception optimisée de ces paramètres permet d’assurer une transmission efficace et adaptée aux contraintes de bande passante d'un canal.