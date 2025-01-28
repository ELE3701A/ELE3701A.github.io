---

exports:
  - format: pdf
    template: plain_latex
    output: ./exports/section2.pdf
downloads:
  - file: ./exports/section2.pdf
    title: PDF
title: Section 2 - Notions fondamentales
abstract: |
  Cette section présente les concepts fondamentaux du traitement des signaux, essentiels pour comprendre et analyser les systèmes de communication. Elle aborde les définitions, classifications et opérations de base des signaux. L’analyse de Fourier y est développée pour explorer la décomposition des signaux en composantes fréquentielles. Les principes de modulation d’amplitude et les systèmes linéaires invariants dans le temps (LTI) sont également discutés, avec un accent sur des notions clés telles que la largeur de bande, la densité spectrale de puissance, l’autocorrélation et les filtres. Enfin, la section introduit les signaux aléatoires, en se concentrant sur les distributions gaussiennes, les moyennes statistiques et le théorème de la limite centrale, établissant ainsi une base solide pour l’étude des signaux dans des environnements variés. 

---

## Signal
 

(def-signal)=
Définition: Signal 
: Un **signal** est une fonction qui transmet des
informations sur un phénomène.

Les signaux constituent les entrées et les sorties des systèmes. Un
signal peut être classé selon différents critères. Les critères que nous
allons examiner sont énumérés ci-dessous.

1.  Signaux à temps continu et à temps discret:

    -   Un **signal à temps continu** est un signal $g(t)$ pour lequel
        la variable indépendante $t$ prend des nombres réels.

    -   Un **signal à temps discret**, noté $g[n]$, est un signal pour
        lequel la variable indépendante $n$ prend ses valeurs dans
        l’ensemble des entiers.

    -   En échantillonnant un signal à temps continu $g(t)$ à des
        instants séparés par $T_E$, nous pouvons définir le signal à
        temps discret $g[nT_E]$. Ici, $n$ est l’indice de temps,
        représentant le $n$ième échantillon.


```{figure} images/signal-class-1.png
:label: signal-class-1
:align: center
Signaux à temps continu et à temps discret (la période d'échantillonnage est de $T_E = 0.5$ unités de temps). 

```


2.  Signaux analogiques et numériques

    -   Un signal dont l’amplitude peut prendre n’importe quelle valeur
        dans une gamme continue est un **signal analogique**.

        -   Cela signifie que l’amplitude d’un **signal analogique**
            peut prendre un nombre (indénombrable) infini de valeurs.

    -   Un **signal numérique**, par contre, est un signal dont
        l’amplitude ne peut prendre qu’un nombre fini de valeurs.

```{figure} images/signal-class-2.png
:label: signal-class-2
:align: center
Signaux analogiques et numériques.

```

3.  Signaux périodiques et non périodiques.

    -   Un **signal périodique** se répète dans le temps ; il suffit
        donc de spécifier le signal dans un intervalle de base appelé
        période, $T_0$, Pour un signal signal périodique :
        $$g(t) = g(t + T_0), \, \forall t$$

    -   Un **signal non périodique** ne se répète pas dans le temps. 

```{figure} images/signal-class-3.png
:label: signal-class-3
:align: center
Signaux périodiques (où $T_0 = 6$ unités de temps) et non périodiques.  

```


4.  Signaux réels et complexes. 

    -   Un **signal réel** prend ses valeurs dans l'ensemble des nombres réels, $g_R(t)\in \mathbb{R}$

    -   Un **signal complexe** prend ses valeurs dans l'ensemble des nombres complexes $g_C(t)\in \mathbb{C}$.

```{figure} images/signal-class-4.png
:label: signal-class-4
:align: center
Signaux réels et complexes.  Le signal réel est l'onde sinusoïdale $g_R(t) = \sin(t)$. Le signal complexe est $g_C(t) = e^{jt} = \cos(t) + j\sin(t)$, dont les parties réelle $( \cos(t)) $ et imaginaire $( \sin(t) )$ sont tracées séparément.
```

 :::{hint} Transformations des signaux réels et complexes : 

- Représentation complexe
Le signal complexe $g_c(t)$ est composé d'une partie réelle $g_R(t)$ et d'une partie imaginaire $g_I(t)$, telles que :
$$
g_c(t) = g_R(t) + j g_I(t),
$$
où $j = \sqrt{-1}$.

-   Partie réelle $g_R(t)$  :
    $$
    g_R(t) = |g_c(t)| \cos(\angle g_c(t)).
    $$

-  Partie imaginaire $g_I(t)$ : 
    $$
    g_I(t) = |g_c(t)| \sin(\angle g_c(t)).
    $$


-  Amplitude du signal complexe
$$
|g_c(t)| = \sqrt{g_R^2(t) + g_I^2(t)}.
$$

- Phase du signal complexe :
$$
\angle g_c(t) = \arctan\left(\frac{g_I(t)}{g_R(t)}\right).
$$
:::

5.  Signaux déterministes et aléatoires.

    -   Dans un **signal déterministe**, à tout instant $t$, la valeur
        de $g(t)$ est donnée comme une valeur réelle ou complexe.

    -   Dans un **signal aléatoire** (ou stochastique), à un instant
        donné $t$, $g(t)$ est une variable aléatoire, c’est-à-dire
        qu’elle est définie par une fonction de densité de probabilité.


```{figure} images/signal-class-5.png
:label: signal-class-5
:align: center
Signaux déterministes et aléatoires. Le signal déterministe $ g(t) = \sin(t)$ est parfaitement prévisible à tout instant $ t $. Chaque valeur est fixée et définie.
Le signal aléatoire est une superposition d'une onde sinusoïdale et d'un bruit gaussien aléatoire. La valeur de $g(t) $ à un instant donné est imprévisible et suit une distribution aléatoire (donc les valeurs sont imprévisibles).
```
 

Notez que toutes ces représentations sont du domaine temporel. Pour pouvoir
comprendre le comportement spectral, nous devons également analyser les
signaux dans le domaine fréquentiel. 

### Représentation fréquentielle des signaux

Dans ce cours, nous utiliserons la transformée de Fourier pour
représenter les signaux, même pour les signaux périodiques

(def-FT)=
Définition: Transformée de Fourier 
:  La transformée de Fourier d’un signal $g(t)$ est
représentée par $G(f)$, et
$$g(t) \iff G(f)$$

:::{hint} Transformation 
```{math}
:label: FT
G(f) = \int_{-\infty}^{\infty} g(t)e^{-j2\pi ft} \, dt
```
:::

:::{hint} Transformation inverse
```{math}
:label: InvFT
g(t) = \int_{-\infty}^{\infty} G(f)e^{j2\pi ft} \, df
```
:::


Propriétés :

 
1.  **homogénéité** de la transformée de Fourier stipule que la transformée de Fourier d'un signal multiplié par un constant scalaire est égale à la transformée de Fourier du signal, également multiplié par cette constante. Si $g(t)$ est un signal avec $g(t) \iff G(f)$ et $a$ est un constant scalaire, :
$$
\mathcal{F}\{a \cdot g(t)\} = a \cdot \mathcal{F}\{g(t)\}= aG(f)
$$
Cela montre que l'échelle d'amplitude dans le domaine temporel est directement reflétée dans le domaine fréquentiel.


2. **superposition** de la transformée de Fourier découle directement de la linéarité. Si un signal $g(t)$ est composé de plusieurs composantes, telles que $g(t) = g_1(t) + g_2(t) + \cdots +g _n(t)$, avec $g_i(t) \iff G_i(f)$, $i \in \{1,2,\ldots, n\}$  sa transformée de Fourier est donnée par :
$$\mathcal{F}\{g(t)\} = \mathcal{F}\{g_1(t)\} + \mathcal{F}\{g_2(t)\} + \cdots + \mathcal{F}\{g_n(t)\} =\sum_{i=1}^nG_i(f).
$$




L'homogénéité et la superposition garantissent **la linéarité** de la transformée de Fourier, permettant ainsi que la transformée d'une combinaison linéaire de signaux, soit égale à la même combinaison linéaire, de leurs transformées respectives.  La linéarité est fondamentale en analyse de Fourier, car elles permettent de décomposer des signaux complexes en une somme de signaux plus simples.  



 
:::{warning} Attention
La transformée de Fourier exprime la composition
fréquentielle d’un signal par une fonction de densité. Ce concept est essentiel, car nous utiliserons la transformation de Fourier pour calculer la largeur de bande d'un signal. 
:::

## Propriétés d’un signal 

 


### Valeur moyenne

:::{hint} Valeur moyenne d’un signal non périodiques
La **valeur moyenne  d’un signal complexé non périodique**, $g(t)$,   est $\overline{g(t)}$ où  
```{math}
:label:energy
\overline{g(t)} = \lim_{T \to \infty} \frac{1}{T} \int_{-T/2}^{T/2} g(t) \, dt \hspace{1cm}  \textrm{Volts}
```
:::

:::{hint} Valeur moyenne d’un signal périodique
La **valeur moyenne  d’un signal complexé périodique**, $g_P(t)$  avec
une période de $T_0$,   est $\overline{g_P(t)}$ est obtenue par    
```{math}
:label:energy
\overline{g_P(t)} =   \frac{1}{T_0} \int_{-T_0/2}^{T_0/2} g_P(t) \, dt \hspace{1cm}  \textrm{Volts}
```
:::

:::{warning} Attention
Concernant la valeur moyenne la linéarité s’applique
$$\overline{g_1(t)+g_2(t)}=\overline{g_1(t)}+\overline{g_2(t).} $$
:::





 

### Énergie

:::{hint} Énergie
L’**énergie d’un signal complexé**, $g(t)$,   est $E_g$ où  
```{math}
:label:energy
E_g = \int_{-\infty}^{\infty} |g(t)|^2 dt  \hspace{1cm}  \textrm{Joules}
```
:::

:::{warning} Attention
Notez que, selon le **Théorème de Parseval**  
$$\int_{-\infty}^{\infty} |g(t)|^2 \, dt = \int_{-\infty}^{\infty} |G(f)|^2 \, df$$
 Donc pour calculer l'énergie d'un signal on utilise le domaine qui est simple à calculer l'expression  d'énergie.
 :::



 
 

### Puissance
:::{hint} Puissance d’un signal non périodiques
La **puissance d’un signal non périodique**, $g(t)$,
est définie par :
```{math}
:label:power
P_g = \lim_{T \to \infty} \frac{1}{T} \int_{-T/2}^{T/2} |g(t)|^2 \ dt    \hspace{1cm} \textrm{Watts}
```
:::

 
:::{hint} Puissance d’un signal périodique
La **puissance d’un signal périodique**, $g_P(t)$ avec
une période de $T_0$ , est définie par 
```{math}
:label:power
 P_g =  \frac{1}{T} \int_{-T_0/2}^{T_0/2} |g_P(t)|^2 \ dt    \hspace{1cm} \textrm{Watts}
```
:::

 Notez que $P_g=\overline{|{g(t)}|^2}$.

:::{warning} Attention
Conversions d’unités 
$$   [10 \times \log_{10}(P_g)] \, \text{dBW ou } [30 + 10 \times \log_{10}(P_g)] \, \text{dBm}$$
:::




### Tension efficace
:::{hint} Tension efficace
La **tension efficace** (*root mean square*; RMS) d’un
signal périodiques  $g_P(t)$ est définie par
```{math}
:label:power
    RMS_g=   \sqrt{P_g} =  \sqrt{\frac{1}{T} \int_{-T_0/2}^{T_0/2} |g_P(t)|^2 \ dt }    \hspace{1cm} \textrm{Volts}
```
:::
:::{warning} Attention
Conversions d’unités 
$$   [20 \times \log_{10}( RMS_g)] \, \text{dBW ou } [30 + 20 \times \log_{10}( RMS_g)] \, \text{dBm}$$
:::


:::{note} Informations supplémentaires pour  **Travail pratique - 1**
```{figure} images/circuit.png
:label: TP1
:align: center
Un circuit d'une seule source avec une résistance

```

 Étant donné un circuit dont la source génère $g(t)$, la puissance instantanée dissipée dans une résistance $R$ est calculée selon la formule 
```{math}
:label:power
 P_{inst} =\frac{ |g(t)|^2 }{R}    \hspace{1cm} \textrm{Watts}
```
et pour le cas normalise, $R=1$, on obtient $|g(t)|^2 $.  En classe, nous nous intéressons principalement aux cas normalisés.
:::

 




### Largeur de bande

(def-bandwith)=
Définition: Largeur de bande 
: La **largeur de bande** correspond à l’étendue des
fréquences disponibles pour la transmission d’un signal. La largeur de bande d’un signal est une mesure de l’étendue de fréquences contenues
dans le signal. En termes simples, elle représente la différence entre
les fréquences les plus élevées et les plus basses et significatives dans
le spectre du signal.

:::{note} Exemple  illustratif :  
Si $|G(f)|^2$ représente la densité spectrale de puissance du signal, la
largeur de bande, $B$ est définie comme l’étendue de fréquences $f$ pour
lesquelles $|G(f)|^2$ est significatif (généralement au-dessus d’un
certain seuil, comme 3 dB en dessous de la valeur maximale). Le critère
de sélection $B$ dépend de la tolérance d’erreur dans une application
particulière. Nous pouvons par $e choisir $B$ comme étant la
largeur de bande qui contient 95% de l’énergie du signal.
```{figure} images/bw1.png
:label: BW1
:align: center
La figure montre la largeur de bande d’un signal, $B=f_\textrm{max}-f_\textrm{min}$
```
:::



:::{warning} Attention
 La largeur de bande doit toujours être définie
uniquement pour les fréquences positives.
:::


Un signal peut être classé comme **bande de base** ou **bande passante** selon sa concentration dans le domaine fréquentiel.

(def-baseband)=
Définition: Signal bande de base  (*baseband*)
: Un **signal bande de base** est caractérisé par un contenu fréquentiel concentré autour de $0$ Hz.  
```{figure} images/bw2.png
:label: BW2
:align: center
Réponse fréquentielle d'un signal en bande de base autour de $f_p$, et la largeur de bande est de $B$ Hz. 
```

(def-passband)=
Définition: Signal bande passante (*passband*)
: Un **signal bande passante** est généralement obtenu après une modulation, c'est-à-dire après multiplication du signal bande de base par une onde porteuse, telle qu'une sinusoïde $cos(2\pi f_p t)$. Le contenu fréquentiel d'un signal bande passante est  concentré autour de la fréquence porteuse, $f_p$ Hz. 
```{figure} images/bw3.png
:label: BW3
:align: center
Réponse fréquentielle d'un signal en bande passante où  la largeur de bande est de  $B=f_\textrm{max}-f_\textrm{min}$
```



:::{warning} Attention
Dans le contexte des systèmes de communication, nous nous
intéressons plus particulièrement à la puissance et à la largeur de
bande des signaux.
:::


## Signaux utiles

### Impulsion de Dirac (*Dirac impulse*)
(def-Dirac)=
Définition: Impulsion de Dirac 
: L’**impulsion de Dirac** est un outil mathématique idéal utilisé pour modéliser une impulsion infiniment brève et intense, qui ne peut pas être réalisée exactement dans la réalité physique.
 ```{math}
:label:power
\delta(t) =
\begin{cases} 
+\infty, & \text{si } t = 0, \\
0, & \text{si } t \neq 0,
\end{cases}
\quad \text{et} \quad \int_{-\infty}^{\infty} \delta(t) \, dt = 1.
```

```{figure} images/dirac-t.png
:label: dirac-t
:align: center
Impulsion de Dirac (en domaine temporel).
```
 

Propriétés: 
 
- Multiplication par l'impulsion de Dirac 
$$    \phi(t)\delta(t-T) = \phi(T)\delta(t-T)$$

- Échantillonnage pour obtenir une seule valeur à $T$
$$\int_{-\infty}^{\infty} \phi(t)\delta(t-T) \, dt = \phi(T) $$ 

- La valeur moyenne, l’énergie et la puissance de l’impulsion de Dirac sont indéfinies

- La transformée de Fourier de $ \delta(t) $ est une fonction constante dans le domaine fréquentiel, donc $\delta(t) \iff 1$,  $\forall f$


```{figure} images/dirac-f.png
:label: dirac-f
:align: center
Impulsion de Dirac (en domaine fréquentiel).
```
 

### Train d'impulsions de Dirac (*Dirac impulse train*)
(def-sinc)=
Définition: Train d'impulsions de Dirac
: La fonction train d'impulsions de Dirac, notée $ \delta_T(t) $, est définie comme une somme infinie d'impulsions de Dirac espacées de $T$ secondes : 
 ```{math}
:label:train
\delta_T(t) = \sum_{n=-\infty}^{\infty} \delta(t - nT)
```
Propriétés: 
 
- La valeur moyenne :  $$\overline{ \delta_T(t)} = \frac{1}{T}$$

- L’énergie : infinie

- La  puissance :  $$P_D = \frac{1}{T}$$

- La transformée de Fourier : $$\mathcal{F}\{\delta_T(t)\} = \frac{1}{T} \sum_{k=-\infty}^{\infty} \delta\left(f - k\frac{1}{T}\right)$$



### Fonction sinc (*Sinc function*)
(def-sinc)=
Définition: Fonction sinc 
: La fonction $\textit{sinc}(t)$ est définie comme suit
 ```{math}
:label:sinc
x(t) = \text{sinc}(t) =
\begin{cases}
\frac{\sin(t)}{ t}, & \text{si } t \neq 0, \\
1, & \text{si } t = 0.
\end{cases}
```
```{figure} images/sinc-t.png
:label: sinc-t
:align: center
Fonction sinc  (en domaine temporel).
```
Propriétés: 
 
- La valeur moyenne :  $$\overline{x(t)}  = \frac{1}{2T} \int_{-T}^{T} \text{sinc}(t) \, dt,$$ et converge vers zéro lorsque $ T \to \infty $.

- L’énergie :  $$E_x = \int_{-T}^{T} |\text{sinc}(t)|^2 \, dt,$$ qui augmente indéfiniment lorsque $T \to \infty $.

- La  puissance :  $$P_x = \lim_{T \to \infty} \frac{1}{2T} \int_{-T}^{T} |\text{sinc}(t)|^2 \, dt = 0.$$

- La transformée de Fourier : $$\mathcal{F}\{\text{sinc}(t)\} = 
\begin{cases}
1, & \text{si } |f| \leq \frac{1}{2}, \\
0, & \text{sinon}.
\end{cases}$$
```{figure} images/sinc-f.png
:label: sinc-f
:align: center
Fonction sinc  (en domaine fréquentiel).
```

 

### L’onde rectangulaire (*Rectangular pulse*)
(def-rec)=
Définition: L’onde rectangulaire
: La fonction rectangulaire $ \text{rect}(t) $, définie sur l'intervalle  $ [-T_0/2, T_0/2] $ , avec une valeur constante  $  a  $ , est donnée par :
 ```{math}
:label:rect
g(t) =
\begin{cases}
a, & \text{si } -\frac{T_0}{2} \leq t \leq \frac{T_0}{2}, \\
0, & \text{sinon}.
\end{cases}
```
```{figure} images/rect-t.png
:label: rect-t
:align: center
Onde rectangulaire  (en domaine fréquentiel).
```

Propriétés: 
 
- La valeur moyenne :  $$\overline{g(t)} = \frac{1}{T_0} \int_{-T_0/2}^{T_0/2} g(t) \, dt = \frac{1}{T_0} \int_{-T_0/2}^{T_0/2} a \, dt = a. $$

- L’énergie : $$E = \int_{-\infty}^{\infty} |g(t)|^2 \, dt = \int_{-T_0/2}^{T_0/2} a^2 \, dt = a^2 T_0.$$

- La  puissance : $$P = \lim_{T \to \infty} \frac{1}{T} \int_{-T_0/2}^{T_0/2} |g(t)|^2 \, dt = \frac{1}{T_0} \int_{-T_0/2}^{T_0/2} a^2 \, dt = a^2.$$

- La transformée de Fourier : $$ G(f) = \mathcal{F}\{g(t)\}  = a T_0 \text{sinc}(\pi f T_0).$$
```{figure} images/rect-f.png
:label: rect-f
:align: center
Onde rectangulaire  (en domaine temporel).
```



 

### Ondes porteuses  (*Carrier waveforms*)
(def-carriers)=
Définition: Ondes porteuses
: La majorité des systèmes de communication utilisent les formes d’onde
cosinus et sinus comme ondes porteuses. Leur fréquence fondamentale est
appelée la fréquence porteuse.

Un cosinus avec fréquence $f_p $ et amplitude $A_p$ est défini comme $c(t) = A_p \cos(2\pi f_p t + \phi)$ où :   

   - $A_p$ est l'amplitude,

   -  $f_p$ est la fréquence en Hertz,

   - $\phi$ est la phase initiale (en radians),

   -  $t$ est le temps.

Propriétés: 
 
- La valeur moyenne :  $$\overline{c(t)} = \frac{1}{T} \int_{0}^{T} A_p \cos(2\pi f_p t + \phi) \, dt = 0 $$

- L’énergie : infinie

- La  puissance : $$P_c = \lim_{T \to \infty} \frac{1}{T} \int_{0}^{T} |c(t)|^2 \, dt = \frac{A_p^2}{2}$$

- La transformée de Fourier : $$C(f) = \mathcal{F}\{c(t)\} = \frac{A_p}{2} \exp(j\phi ) \delta(f - f_p) + \frac{A_p}{2} \exp(-j \phi)  \delta(f + f_p),$$


Pour un sinus avec  les mêmes paramètres   $s(t) = A_p \sin(2\pi f_p t + \phi)$  

Propriétés: 
  
-  La valeur moyenne : 0
 
- L’énergie : infinie

- La  puissance :  $$P_s =   \frac{A_p^2}{2}$$

- La transformée de Fourier : $$S(f) = \mathcal{F}\{s(t)\} = \frac{A_p}{2j} \exp(j\phi ) \delta(f - f_p) -  \frac{A_p}{2j} \exp(-j \phi)  \delta(f + f_p),$$


:::{note} Exemple  illustratif :
Le signal est défini comme $ g(t) = A \cos(2\pi f_p t)$ où $A$  est l'amplitude du signal, et $f_p$ est la fréquence porteuse (en Hz). 


La transformée de Fourier du signal $ g(t) $  est 
$$  A\cos(2\pi f_p t)  \iff \frac{A}{2} \left[ \delta(f - f_p) + \delta(f + f_p) \right]$$ 
Donc, la transformée de Fourier montre deux impulsions à  $f = f_p $ et $ f = -f_p $. Ainsi, la largeur de bande passante est effectivement 0 Hz, autour de $f_p$.
Son énergie pour une périod  de $ T_0 = \frac{1}{f_p}$ est définie par 
$$
E_g = \int_{-T_0/2}^{T_0/2} A^2 \cos^2(2\pi f_p t) \, dt
$$

En utilisant l'identité trigonométrique $ \cos^2(x) = \frac{1}{2} (1 + \cos(2x)) $, on obtient 
$$
E_g = \int_{-T_0/2}^{T_0/2} \frac{A^2}{2} \, dt = \frac{A^2}{2} T_0
$$
car l'intégrale de $ \cos(4\pi f_p t) $ sur toute la durée est nulle car $ \cos(4\pi f_p t) $ oscille symétriquement.. 


Sa puissance  est donnée par 
$$
P_g = \frac{1}{T_0} \int_{-T_0/2}^{T_0/2} g^2(t) \, dt = \frac{1}{T_0} \int_{-T_0/2}^{T_0/2} \frac{A^2}{2} \, dt = \frac{A^2}{2}
$$
:::


## Système


(def-system)=
Définition: Système
: Du point de vue d'un ingénieur en communication, un **système** est une loi qui attribue des signaux de sortie à divers signaux d'entrée.  
Le point le plus important dans la définition d'un système est que sa sortie doit être définie de manière unique pour toutes les entrées légitimes.


Chaque système possède **une entrée** ($x(t)$) **une sortie** $(y(t))$ et **une fonction de
transfert** $\left(\mathcal{T(\cdot)}\right)$, ou $y(t)=\mathcal{T}(x(t))$.

```{figure} images/system-gen.png
:label: system1
:align: center
Représentation d`un système

```

:::{important} Exemple pratique : 
Un circuit électrique avec une source de tension en entrée et un courant dans une certaine branche est un système.
:::
 
Un système peut être **variant** ou  **invariant** dans le temps. De plus, un système peut être **linéaire** ou **non linéaire**. leurs explications sont données ci-dessous. 


### Système invariant dans le temps (*Time Invariant System*) 
Un système est **invariant dans le temps** si sa réponse à une entrée  ne change pas lorsque l'entrée est décalée dans le temps. Si l'on considère un système $\mathcal{T}(\cdot)$ avec une entrée $x(t)$ et une sortie $y(t)$, (i.e. $y(t)=\mathcal{T}(x(t))$), le système est invariant dans le temps si 
```{math}
:label: time-invariance
y(t-t_0) = \mathcal{T}(x(t- t_0))
```


### Système variant dans le temps (*Time Varying System*) 

Le système est **variant dans le temps** quand l'équation {eq}`time-invariance`  n'est pas applicable.
 
 :::{note} Exemples illustratifs : 
- Le système $y(t) = 2x(t)$  est invariant dans le temps, car pour l'entrée $x(t-t0)$  la sorite est $y(t-t_0)$.
- Le système $y(t) = t \cdot x(t)$  est variant dans le temps,  car pour l'entrée $x(t-t0)$  la sorite est $y(t-t_0) \neq  (t-t_0)x(t-t_0)   $.
 :::
 




### Système linéaire (*Linear System*)

Un système $\mathcal{T(\cdot)}$ est linéaire s'il respecte les propriétés suivantes :

1.    **homogénéité** : si une entrée $x(t)$ produit une sortie $y(t)$, i.e.,$y(t)=\mathcal{T}(x(t))$,  la sortie de $ax(t)$  pour un scalaire $a$ produit $ay(t)$. 
 
2. **superposition** : si un signal $x(t)$ est composé de plusieurs composantes, telles que $$x(t) = x_1(t) + x_2(t) + \cdots +x _n(t),$$ où $y_i(t) = \mathcal{T} (x_i(t))$, $i \in \{1,2,\ldots, n\}$,    
$$y = \mathcal{T}\{x_1(t)\} + \mathcal{T}\{x_2(t)\} + \cdots + \mathcal{T}\{x_n(t)\} =\sum_{i=1}^ny_i(t).
$$

Notez que la transformée de Fourier peut être interprétée comme un système linéaire.


#### Système linéaire invariant dans le temps (*Linear time invariant*; LTI) 

Un système est **linéaire invariant dans le temps** (LTI) si les propriétés de linéarité et d'invariance dans le temps sont satisfaites. Ce système est défini simplement par sa **réponse impulsionnelle**, $h(t)$, ou sa **réponse fréquentielle** $H(F)$ où $$h(t) \iff H(f) $$.

La sortie $y(t) $ est obtenue par la **convolution** de l'entrée $x(t) $ avec la réponse impulsionnelle $ h(t) $ où 
$$y(t) = x(t) * h(t) = \int_{-\infty}^{\infty} x(\tau) h(t - \tau) \, d\tau$$.


 ```{figure} images/system-gen-lti.png
:label: fig:LTI
:align: center
Transmission d'un signal à travers un système linéaire invariant dans le temps (LTI)

```



:::{note} Exemple illustratif : **Filtres : passe-bas, passe-bande et passe-haut** 

Un **filtre**, un dispositif qui sélectionne ou atténue certaines fréquences d’un signal, est un système LTI. Il existe différents types de filtres en fonction de leur **bande passante**.  Notez que nous utilisons ici le terme bande passante (au lieu de largeur de bande) car il indique les fréquences permises de laisser passer.


 - Un filtre **passe-bas** laisse passer les fréquences inférieures à une fréquence de coupure $ f_c$ et atténue les fréquences supérieures. Sa réponse fréquentielle est typiquement donnée par :
$$
H(f) = 
\begin{cases} 
1, & |f| \leq f_c, \\
0, & |f| > f_c.
\end{cases}
$$
avec la **bande passante :** $[0, f_c]$.

 
 - Un filtre **passe-bande** (ou bande passante) laisse passer une bande de fréquences entre $ f_{\text{min}} $ et $ f_{\text{max}} $, et atténue les autres fréquences. Sa réponse fréquentielle est :
$$
H(f) = 
\begin{cases} 
1, & f_{\text{min}} \leq |f| \leq f_{\text{max}}, \\
0, & \text{ailleurs}.
\end{cases}
$$
avec la **bande passante :** $[f_{\text{min}}, f_{\text{max}}]$.

 
 - Un filtre **passe-haut** laisse passer les fréquences supérieures à une fréquence de coupure $f_c $ et atténue les fréquences inférieures. Sa réponse fréquentielle est :
$$
H(f) = 
\begin{cases} 
1, & |f| \geq f_c, \\
0, & |f| < f_c.
\end{cases}
$$
avec la **bande passante :** $[f_c, \infty[$.
:::


### Système non linéaire (*Nonlinear System*)

  Si un système ne respecte pas l'une ou l'autre des propriétés d'homogénéité ou de superposition, il est non linéaire.Leur réponse peut varier de manière non proportionnelle ou non additive en fonction des entrées. 





:::{note} Exemple  illustratif :    

Soit un système défini par la relation suivante : $ y(t) = x^2(t) $. 
Pour homogénéité,  si une entrée $  x(t)  $  produit une sortie  $ y(t)  $ , alors une entrée multipliée par une constante  $ a  $  devrait produire une sortie multipliée par cette même constante $  a$, mais
$
y_{\text{scaled}}(t) =   a^2 \cdot x^2(t) \neq x^2(t).
$
De plus, pour la superposition si $ x_1(t)$ et $ x_2(t)$ produisent respectivement $ y_1(t) $ et $y_2(t)$, alors la réponse à la somme $x_1(t) + x_2(t)$ devrait être $ y_1(t) + y_2(t) $. Cependant, dans notre cas :
$
y(t) = (x_1(t) + x_2(t))^2 = x_1^2(t) + 2x_1(t)x_2(t) + x_2^2(t)
$
Donc ce système  est non linéaire car il ne respecte pas les deux propriétés.

:::


#### Modulation - un système non linéaire
La modulation est le processus par lequel une onde portesue 
$c(t) = A_p \cos(2 \pi f_p t)$
est multiplié par un signal de message $ m(t)$. Cela permet d’intégrer l’information du message dans une onde porteuse adaptée à la transmission.

Pour une modulation d'amplitude (AM), le signal modulé s'écrit :
$$\psi(t) = [A_p + m(t)] \cos(2\pi f_p t),$$
où $ A_p $ est l’amplitude de la porteuse et $ f_p $ sa fréquence.

Dans ce cas, le signal d’information $ m(t) $ module l’amplitude de l’onde porteuse $\cos(2\pi f_p t) $. Soit  $m(t)$ a un  largeur de bande $ B $ Hz avec une réponse fréquentielle $M(f)$. La reponse  fréquentielle du signal modulé sera
$$  
\Psi(f) = \frac{A_p}{2} \delta(f - f_p) + \frac{A_p}{2} \delta(f + f_p) +\frac{1}{2} \left[ M(f - f_p) + M(f + f_p) \right].
$$
**Donc la largeur de bande du signal modulé est de $2B$ Hz.**
 ```{figure} images/mod1.png
:label: fig:mod1
:align: center
Une illustration de la modification de la largeur de bande et de l'amplitude

```

:::{warning} Attention
 Lorsqu'un signal est modulé, son énergie change en raison de l'ajout de la porteuse et du déplacement spectral.
:::


## Probabilité 

### Probabilité et la règle de Bayes 
Les définitions ci-dessous forment la base de la théorie des probabilités, utilisée dans de nombreux domaines comme les statistiques, l'apprentissage automatique et les communications. Elles permettent de quantifier les incertitudes et d'effectuer des prédictions basées sur des observations.  Nous les utiliserons principalement pour calculer l'énergie et la puissance des signaux.

Soit $N$ le nombre total d'événements dans un espace d'échantillonnage. Les notions clés associées à la probabilité sont expliquées ci-dessous :

- Un événement $A$ correspond à un ensemble d'issues spécifiques parmi les $N$ issues possibles. 
Le nombre de fois où l'événement $A$ se réalise est noté comme $N(A)$, qui indique **la réalisation** de $A$. 

- La **probabilité** d'un événement $A$ est définie comme la limite, lorsque $N$ tend vers l'infini, du rapport entre $N(A)$ et $N$ :
$$
P(A) = \lim_{N \to \infty} \frac{N(A)}{N},
$$
avec 
$$
0 \leq P(A) \leq 1.
$$
Cela signifie que la probabilité est une mesure entre 0 et 1 de la fréquence relative de réalisation de $A$.

- La **probabilité conditionnelle** de $A$ sachant que $B$ est réalisé est donnée par :
$$
P(A \mid B) = \frac{P(A \cap B)}{P(B)},
$$
où $P(A \cap B)$ représente la probabilité de la conjonction des événements $A$ et $B$, et $P(B) > 0$.

- **La règle de Bayes** nous permet de calculer la probabilité conditionnelle de $A$ sachant $B$ en inversant la condition :
$$
P(A \mid B) = \frac{P(B \mid A) P(A)}{P(B)}.
$$
Cette règle est particulièrement utile dans les problèmes où il est plus facile de calculer $P(B \mid A)$ que $P(A \mid B)$ directement.
 
 

 
 
### Variables aléatoires

Une **variable aléatoire** nous permet de modéliser des événements aléatoires avec une règle d'association de valeurs. La fonction de distribution cumulative est un outil clé pour analyser les probabilités associées à ces variables, en respectant des propriétés fondamentales comme la continuité et la monotonie.

(def-Randvariable)=
Définition: Variable aléatoire 
: Une **variable aléatoire** résulte de l'application d'une règle par laquelle une valeur est assignée à un événement. 

:::{note} Exemple  illustratif :  
Soit $X$, une variable aléatoire définie comme étant le résultat obtenu en lançant un dé. 
- Dans ce cas, $X \in \{1, 2, 3, 4, 5, 6\}$.
:::




(def-CDF)=
Définition: Fonction de distribution cumulative  
: Fonction de distribution cumulative (*Cumulative Distribution Function*; CDF)}
La fonction de distribution cumulative (ou CDF, pour Cumulative Distribution Function) est définie comme  :
$$
F_X(x) = P(X \leq x),
$$
où $F_X(x)$ représente la probabilité que la variable aléatoire $X$ soit inférieure ou égale à une valeur donnée $x$.

Propriétés :

1. $0 \leq F_X(x) \leq 1$, pour tout $x$.

2.  $F_X(\infty) = 1$.
    
 3.    $F_X(-\infty) = 0$.
  
  4. $F_X(x_1) \leq F_X(x_2)$, pour $x_1 \leq x_2$ (c'est-à-dire, $F_X(x)$ est une fonction non décroissante).
  


(def-PDF)=
Définition: Fonction de densité de probabilité
: La **fonction de densité de probabilité** (*Probability Density Function*; PDF) caractérise la distribution des probabilités pour une variable aléatoire continue. La PDF d'une variable aléatoire $X$ est définie comme étant la dérivée de la fonction de distribution cumulative (CDF) $F_X(x)$ :
$$
p_X(x) = \frac{dF_X(x)}{dx}.
$$

 

Propriétés :

1.  $p_X(x) \geq 0$, pour tout $x$. \\
          
2. L'intégrale de $p_X(x)$ sur tout l'espace est égale à 1 :
    $$
    \int_{-\infty}^{\infty} p_X(x) \, dx = 1.
    $$
   
3.  La CDF $F_X(x)$ peut être exprimée comme l'intégrale de la PDF :
    $$
    F_X(x) = \int_{-\infty}^{x} p_X(\alpha) \, d\alpha.
    $$



### Les moyennes statistiques

Les moyennes statistiques sont des outils fondamentaux pour décrire et analyser les propriétés d'une variable aléatoire. Ces outils sont essentiels pour caractériser le comportement statistique des systèmes aléatoires. 

1. **La valeur moyenne** (ou espérance ) d'une variable aléatoire $X$ est donnée par :
$$
\overline{X} = E[X] = \int_{-\infty}^\infty x \, p_X(x) \, dx,
$$
où  $E[X]$ représente l'espérance de $X$,  $p_X(x)$ est sa PDF. Cette moyenne représente la valeur centrale attendue de $X$.

2. Si une fonction $g(X)$ est appliquée à une variable aléatoire $X$, **la moyenne de cette fonction** $g(X)$ est donnée par :
$$
E[g(X)] = \int_{-\infty}^\infty g(x) \, p_X(x) \, dx.
$$
Cela permet de calculer l'espérance de transformations non linéaires de $X$.

3. **La variance** mesure la dispersion d'une variable aléatoire autour de sa moyenne. Elle est définie par :
$$
\sigma_X^2 = E[(X - \overline{X})^2] = \int_{-\infty}^\infty (x - \overline{X})^2 \, p_X(x) \, dx,
$$
où $\sigma_X^2$ est la variance de $X$, et $\overline{X}$ est la valeur moyenne de $X$.

 

 

### Distribution gaussienne (normal)



La distribution gaussienne (ou loi normale) est l'une des distributions les plus importantes en probabilité et statistiques.

Propriétés : 

- Fonction de densité de probabilité (PDF) d'une variable aléatoire $X$ suivant une distribution gaussienne est donnée par :
$$
p_X(x) = \frac{1}{\sigma \sqrt{2\pi}} e^{-\frac{(x - \mu)^2}{2\sigma^2}},
$$
où  $\mu$ est la moyenne (ou valeur moyenne) de la distribution,  $\sigma^2$ est la variance, et $\sigma$ est l'écart type (standard deviation).

 ```{figure} images/gaussian.png
:label: fig:gaussiam
:align: center
Une distribution gaussienne avec une moyenne $\mu$ et une variance $\sigma^2=4$.
```


%%%% Insert Gaussian distribution here

- Pour une variable aléatoire $X$ suivant une distribution gaussienne, la probabilité que $X$ soit supérieure à une valeur $a$ :
    $$
    P(X > a) = \int_a^{\infty} \frac{1}{\sigma \sqrt{2\pi}} e^{-\frac{(x - \mu)^2}{2\sigma^2}} dx = Q\left(\frac{a - \mu}{\sigma}\right),
    $$
    où $Q(z)$ est la fonction Q, définie par :
    $$
    Q(a) = \int_a^{\infty} \frac{1}{\sqrt{2\pi}} e^{-\frac{x^2}{2}} dx.
    $$
- La probabilité que $X$ soit inférieure ou égale à une valeur $a$ :
    $$
    P(X \leq a) = \int_{-\infty}^a \frac{1}{\sigma \sqrt{2\pi}} e^{-\frac{(x - \mu)^2}{2\sigma^2}} dx = 1 - Q\left(\frac{a - \mu}{\sigma}\right).
    $$
 
 

:::{note} Théorème de la limite centrale

 Le théorème de la limite centrale illustre pourquoi la distribution normale est omniprésente dans les applications pratiques, car elle décrit le comportement asymptotique des sommes de variables aléatoires indépendantes.

Soit $X_1, X_2, \dots, X_n$ une suite de variables aléatoires indépendantes, définies sur le même espace de probabilité, et suivant la même distribution.

Définissons :
$$
V = X_1 + X_2 + \dots + X_n.
$$

Selon le théorème de la limite centrale, lorsque $n$ tend vers l'infini, la distribution de la somme $V$ tend vers une distribution gaussienne, quelle que soit la distribution d'origine des $X_i$, à condition que la moyenne et la variance de chaque $X_i$ soient finies.

La densité de probabilité de $V$ est donnée par :
$$
p_V(v) = \frac{1}{\sigma_V \sqrt{2\pi}} e^{-\frac{(v - \mu_V)^2}{2\sigma_V^2}},
$$
où  $\mu_V = n \cdot \mu$ est la moyenne de la somme, et $\sigma_V^2 = n \cdot \sigma^2$ est la variance de la somme.


Le théorème montre que la distribution gaussienne joue un rôle clé dans l'étude des processus aléatoires :
 -  Même si les variables aléatoires de départ ($X_i$) ne sont pas gaussiennes, la somme de ces variables tend vers une distribution gaussienne.
- Le théorème de la limite centrale explique pourquoi la distribution du bruit thermique dans les systèmes de communication peut être modélisée par une distribution gaussienne, car ce bruit résulte de la somme des mouvements aléatoires indépendants des électrons au niveau microscopique.

 :::





## Signaux aléatoires
(def-Randsignal)=
Définition: Signal  aléatoire 
: Un **signal aléatoire** est une réalisation particulière ou une trajectoire d’un processus aléatoire.
 

 (def-Randsignal)=
Définition: Processus  aléatoire 
:  Un **processus aléatoire** peut être défini simplement comme un ensemble de variables aléatoires. 
On dit d’un processus aléatoire qu’il est stationnaire au sens strict lorsque les moyennes statistiques d’ensemble ne changent pas dans le temps. Lorsqu’on ne considère que les deux premiers moments, on parlera de stationnarité au sens large. 

Un processus aléatoire est **ergodique** lorsque les moyennes statistiques d’ensemble sont égales aux moyennes statistiques dans le temps de chacune des variables qui le composent. 


:::{note} Exemple  illustratif :  
Considérons cent personnes lançant simultanément un dé de façon répétitive (et honnête). 
- Le processus ainsi constitué est assurément stationnaire car d’une répétition à l’autre les conditions sont les mêmes. Le processus est également ergodique car une personne jouant plusieurs fois, ou plusieurs personnes jouant une fois sont des événements aléatoires équivalents. 
:::

 
### Autocorrélation


**L’autocorrélation** d’un processus aléatoire $x(t)$ mesure la similitude entre les valeurs du processus à deux instants différents, séparés par un décalage $\tau$. 
Pour le décalage temporel $\tau$, elle est définie par l’expression suivante :
$$
R_X(\tau) = E[x(t)x(t + \tau)].
$$
Cette équation  analyse la corrélation temporelle des valeurs du processus.

 ```{figure} images/autocorr.png
:label: fig:psd
:align: center
Une illustration de l'autocorrélation d'une réalisation d'un signal aléatoire

```



### Spectre de densité de puissance 

Le **spectre de densité de puissance** (*power spectral density*; PSD) est un outil clé pour analyser la répartition de la puissance d'un signal dans le domaine fréquentiel.

La puissance moyenne d'un signal aléatore peut être exprimée e à l'aide de la fonction de densité de puissance $S_g(f) $, définie comme :
$$
P_g =  \lim_{T \to \infty} \frac{E_g}{T} = \int_{-\infty}^\infty \lim_{T \to \infty}  \frac{|G(f)|^2}{T} = \int_{-\infty}^\infty S_g(f) \, df,
$$
où $S_g(f) $ est le spectre de densité de puissance obtenu en prenant la limite lorsque $T \to \infty $. Notez que   $|G(f)|^2/T $ représente la densité spectrale de puissance. 
\end{itemize}




La puissance moyenne du signal dans une bande de fréquence spécifique $[f_1, f_2] $ est donnée par :
$$
P_{[f_1, f_2]} = {\textcolor{red}2} \times \int_{f_1}^{f_2} S_g(f) \, df.
$$

 ```{figure} images/psd.png
:label: fig:psd
:align: center
Une illustration de la puissance moyenne du signal dans la bande $[f_1, f_2] $

```



%\4. Cas des signaux périodiques
%Pour un signal périodique $g(t) $ de période $T_0 $, le spectre de densité de puissance est donné par :
%$$
%S_g(f) = \sum_{n=-\infty}^\infty |D_n|^2 \delta\left(f - \frac{n}{T_0}\right),
%$$
%où :
%\begin{itemize}
%    \item $D_n $ représente les coefficients de Fourier du signal périodique,
%    \item $\delta(f) $ est la fonction delta de Dirac.
%\end{itemize}

 




:::{warning} Attention
- En intégrant $ S_g(f)$  sur une plage de fréquences donnée, on peut calculer la puissance dans cette plage. 

- La largeur de bande est déterminée en identifiant la plage de fréquences contenant une proportion significative de la puissance du signal. Ces outils sont essentiels pour l’analyse, la conception, et l’optimisation des systèmes de communication et des applications de traitement du signal.
:::








### Relation entre autocorrélation et spectre de densité de puissance
L’autocorrélation et le spectre de densité de puissance   d’un signal aléatoire sont reliés par une transformée de Fourier :
$$
R_g(\tau) \iff S_g(f),
$$
où $R_g(\tau) $ est la fonction d’autocorrélation dans le domaine temporel et  $S_g(f) $ est le spectre de densité de puissance dans le domaine fréquentiel.


Cette relation signifie que :
- La transformée de Fourier de la fonction d’autocorrélation donne le spectre de densité de puissance.
- La transformée inverse du spectre de densité de puissance donne la fonction d’autocorrélation.





:::{warning} Attention
 
Pour les signaux aléatoires, l'autocorrélation et le spectre de densité de puissance permettent de :

-  Quantifier la dépendance temporelle des signaux via la fonction d’autocorrélation $R_X(\tau) $,
-  Analyser la répartition de l’énergie ou de la puissance des signaux dans le domaine fréquentiel à l’aide de $S_g(f) $.
 
  
:::




:::{note} Exemple  illustratif :  
Dans ce cas, seule une proportion donnée (par exemple 90 % ou 99 %) de la puissance totale est considérée. La largeur de bande est déterminée en trouvant l’intervalle $[f_1, f_2] $ tel que :
$$
2 \times \int_{f_1}^{f_2} S_g(f) \, df = \alpha P_g,
$$
où $ \alpha $ est la proportion désirée (e.g. $\alpha = 0.99 $ pour 99 %).
:::


### Filtrage d’un signal aléatoire



Lorsqu’un signal aléatoire traverse un système linéaire invariant dans le temps (LTI), le comportement du signal en sortie peut être analysé à l’aide des propriétés du système, caractérisé par sa réponse impulsionnelle $ h(t) $  ou sa réponse fréquentielle $ H(f) $.

Soit le spectre de densité de puissance d’entrée représenté par $ S_x(f)$, et le système est caractérisé par $h(t)$, la réponse impulsionnelle (ou $ H(f) $, la réponse fréquentielle)

Le spectre de densité de puissance en sortie est donné par :
$$
S_y(f) = S_x(f) |H(f)|^2.
$$

 ```{figure} images/psd-filtering.png
:label: fig:psd-filtering
:align: center
La sortie d'un système LTI pour une entrée $x(t)$ avec un spectre de densité de puissance de  $S_x(f)$. 
```



:::{note} Exemple  illustratif :  
Considérons un signal aléatoire avec un spectre de densité de puissance d’entrée donné par :
$$
S_x(f) =
\begin{cases}
10, & \text{si } |f| \leq 100 \, \text{Hz}, \\
0, & \text{sinon}.
\end{cases}
$$

Le signal passe à travers un filtre passe-bas idéal caractérisé par sa réponse fréquentielle :
$$
H(f) =
\begin{cases}
2, & \text{si } |f| \leq 50 \, \text{Hz}, \\
0, & \text{sinon}.
\end{cases}
$$


Le spectre de densité de puissance en sortie est donné par :
$$
S_y(f) =
\begin{cases}
40, & \text{si } |f| \leq 50 \, \text{Hz}, \\
0, & \text{sinon}.
\end{cases}
$$


La puissance totale en sortie peut être calculée en intégrant $ S_y(f) $ sur toutes les fréquences :
$$
P_y = \int_{-\infty}^\infty S_y(f) \, df = 2 \times \int_{0}^{50} 40 \, df  = 40 \cdot 100 = 4000 \, \text{W}.
$$
:::

## Resumé
Dans cette section, nous abordons **O2** *application des outils d’analyse spectrale pour résoudre des problèmes liés aux procédures de transmission*. L’analyse spectrale joue un rôle fondamental dans la conception et l’optimisation des systèmes de communication. En représentant les signaux dans le domaine fréquentiel, les ingénieur.e.s peuvent mieux comprendre le contenu spectral et le comportement des signaux transmis. Cette approche facilite l’identification des éléments essentiels tels que la bande passante, la distribution de puissance et le contenu fréquentiel. Les outils spectraux permettent également de concevoir des filtres efficaces pour éliminer les fréquences indésirables, allouer les ressources de manière optimale et réduire les interferences. Ces techniques sont indispensables pour garantir une transmission fiable et efficace des signaux dans les réseaux de communication modernes.

%Power spectral density - kutusu ekle
%  pdf downloading ekle
% folding ekle
%phython kodu ekle
 %todo 1. SNRdB conversion
 %todo 2. enegry formulunu ver
 %todo 3. Table of Fourier transform - linearity
 %todo 4. Euler Formula e^{j\theta} = \cos\theta + j\sin\theta 
 %todo 5. Modulasyon sekil koy
 %todı 6. Sinyal sekillerini kendin ciz
 %todo 7. Mohamedin kodlarina bak
 %todo 8. Demodulasyon sekli koy
 %todo 9. Phase aciklamasi koy
 %todo 10. FDMA ekle
 %todo 11. Module sinyal enerjisi ekle
 %todo 12. Butun sekilleri degistir
 %todo 13. cosinus enerji hesabini ekle
 %todo 14. aide mémoire - kontrol et
 %todo 15. Fourier transform lable ekle
 %todo 16. Giristeki konularla baglantisini kontrol et
 %todo 17. tikz bak



