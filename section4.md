---

exports:
  - format: pdf
    template: plain_latex
    output: ./exports/section4.pdf
downloads:
  - file: ./exports/section4.pdf
    title: PDF
title: Section 4 - Procédures de transmission 
abstract: |
  Section 4 présente les principales techniques de modulation essentielles pour l’adaptation des signaux aux caractéristiques du canal de transmission. Elle commence par la modulation d’amplitude, qui consiste à faire varier l’amplitude de l’onde porteuse en fonction du signal modulant, incluant des variantes telles que la modulation à double bande latérale (DSB), la modulation à bande latérale unique (SSB)  et la modulation d’amplitude en quadrature (QAM). Ensuite, la section aborde la modulation d’angle, qui regroupe la modulation de fréquence (FM) et la modulation de phase (PM), deux techniques qui modifient respectivement la fréquence et la phase de la porteuse pour améliorer la robustesse aux interférences et aux distorsions. Enfin, la section explore les principes de la modulation numérique, où l’information est transmise sous forme de symboles discrets, englobant des schémas tels que ASK (Amplitude Shift Keying), PSK (Phase Shift Keying) et QAM numérique. L’objectif **O4** est de proposer les techniques de modulation les plus adaptées en fonction des caractéristiques du canal et du type d’information à transmettre, en mettant en lumière leurs avantages et leurs contraintes dans divers contextes de communication.

---

 


## Procédures de transmission

La modulation est une étape essentielle des procédures de transmission dans les systèmes de communication modernes. Elle permet d’adapter le signal aux caractéristiques du canal, d'améliorer la qualité de transmission et d’optimiser l’utilisation du spectre. Différents types de modulation sont utilisés en fonction des besoins et des contraintes spécifiques de la transmission, qu'elle soit analogique ou numérique.
 

(def-Modulation)=
Définition: Modulation 
: La **modulation** est une procédure de transmission qui consiste à superposer un signal d'information our une onde porteuse, $c(t)$, ou un train d'impulsions composé de $p(t)$, afin de permettre son acheminement à travers un canal de communication. Elle est indispensable pour configurer l'utilisation du spectre, réduire les interférences et adapter le signal aux caractéristiques du support de transmission. 


(def-Message)=
Définition: Signal de message   
: Le **signal de message**, $m(t)$, représente l’information avant toute modification ou modulation. Il peut être analogique  (continu dans le temps et en amplitude, comme la musique) ou numérique (discret en amplitude et en temps, comme des données binaires). Le signal $m(t)$  est souvent en bande de base (i.e. ses composantes fréquentielles sont centrées autour de $0$ Hz) avec une largeur de bande de $B$ Hz.  

 ```{figure} images/sec4-message.png
:label: sec4-message
:align: center
Un signal de message en bande de base avec une largeur de bande de $B$ Hz.  
```
:::{warning} Attention
Lorsque les signaux des messages sont aléatoires, nous devons utiliser leur spectre de densité de puissance, $S_m(f)$, pour déterminer sa largeur de bande. 
:::
 
La modulation peut être réalisée en utilisant soit une onde porteuse, soit un train d'impulsions.

(def-OndePorteuse)=
Définition: Onde Porteuse   
:  Une **onde porteuse** (*carrier waveform*), $c(t)$ (e.g.  $\cos(2\pi f_p t)$), est un signal sinusoïdal de fréquence $f_p$ utilisé en modulation pour transporter un signal de message en modifiant son amplitude, sa fréquence ou sa phase. **L'amplitude**, la **phase** ou la **fréquence** de la forme d'onde porteuse est modifiée en fonction du signal du message, $m(t)$, avec une largeur de bande $B$. La fréquence de la porteuse doit être choisie  plus grande que la largeur de bande, $$f_p > B$$

  
```{figure} images/sec4-DSB-SC.png
:label: sec4-message
:align: center 
Un signal de message et l'onde porteuse. Le signal modulé est $m(t)c(t)$. (Voir: Exemples Intéractifs: Procédures de transmission - Modulation DSB-SC)
```
 
(def-TrainImpulse)= 
Définition: Train d’impulsions 
:  Il est également possible de transmettre des signaux sans utiliser une porteuse haute fréquence. Dans ce cas, un **train d'impulsions** est nécessaire;
$$
\sum_{n=-\infty}^{\infty} p(t - nT_s)
$$
 Notez que la période du train d'impulsions est notée $ T_s $, et elle sera utilisée pour représenter la période du symbole. 





### Catégories de modulation
Les types de modulation peuvent être classés en fonction de la nature du signal de message. Si le signal de message  est **continu dans le temps et en amplitude**, le système est appelé modulation analogique. En revanche, si le message **discret en amplitude et en temps**, il est qualifié de modulation numérique.

Les types de modulation peuvent également être classés en fonction de la présence d’une fréquence porteuse. 
La transmission en **bande de base** signifie que le signal est envoyé directement sans être transposé sur une fréquence porteuse. Cette technique est généralement utilisée pour les transmissions sur des distances courtes, comme les réseaux informatiques ou certaines applications industrielles. Contrairement à la bande de base, **la transmission par onde porteuse** repose sur une porteuse haute fréquence $f_p$, ce qui permet d’envoyer les signaux sur de longues distances et d’optimiser l’utilisation du spectre.


```{table} Catégories de modulation
:name: tab-categories-modulation
:align: center
| **Catégories de modulation** | **Transmission en bande de base (avec train d'impulsion)** | **Transmission par onde porteuse** |
|------------------------------|----------------------------------|----------------------------------|
| **Analogique**               | **Modulation d’amplitude** : « PAM : Pulse Amplitude Modulation »  <br> **Modulation de durée** : « PWM : Pulse Width Modulation » <br> **Modulation de position** : « PPM : Pulse Position Modulation » | **Modulation linéaire (Modulation d’amplitude)** : « AM : Amplitude Modulation » et ses variations <br> **Modulation d’angle** : « PM : Phase Modulation » <br> « FM : Frequency Modulation » |
| **Numérique**                | **Modulation par impulsions codées** : « PCM : Pulse Code Modulation » <br> **Codage de ligne** : « Line coding » | **Modulations binaires** : « FSK : Frequency Shift Keying » <br> « BPSK : Binary Phase Shift Keying » <br> **Modulations multiniveaux (M)** : « QPSK : Quadrature Phase Shift Keying » <br> « M-FSK : Frequency Shift Keying » <br> « M-QAM : M-ary Quadrature AM » <br> « M-PSK : M-ary Phase Shift Keying » |
```
 

### Critères de performance des techniques de modulation

Les deux critères de performance sont l'efficacité énergétique et l'efficacité spectrale. 

(def-EE)= 
Définition: L’efficacité énergétique
:  **L'efficacité énergétique** (*energy efficiency*) est l'énergie (puissance) du signal de message divisée par l'énergie (puissance) du signal modulé 
$$
\eta_{\textrm{efficacité-énergétique}} = \frac{\textrm{Puissance utile}}{\textrm{Puissance totale}}= \frac{E[ | m(t) |^2 ]}{E[ | \varphi(t) |^2 ]}
$$
L’efficacité énergétique mesure de la capabilité d’un système à utiliser efficacement l’énergie pour transmettre des signaux de message.  

(def-SE)= 
Définition: L’efficacité spectrale
: **L’efficacité spectrale** (*spectral efficiency*) mesure la quantité de signaux de message transmises par unité de largeur de bande. Pour les systèmes de modulation analogiques, elle est obtenue en divisant la largeur de bande du signal de message par la largeur de bande du signal modulé.  
$$
\eta_{\textrm{efficacité-spectrale}} = \frac{B}{\textrm{Largeur de bande de } \varphi(t)}  
$$
Pour les systèmes de modulation numérique, nous le définirons comme le nombre de bits transmis par Hertz [bits/sec/Hz], qui change en fonction du type d'image et du type de modulation sélectionnés (plus de détails à venir). 

## Catégories de modulation par onde porteuse

La modulation par onde porteuse peut affecter **l’amplitude**, **la phase** ou **la fréquence** d’une onde porteuse pour transmettre un signal de message, qu’il soit **analogique** ou **numérique**. 

Le signal modulé, $\varphi(t)$, par une onde porteuse  est exprimée sous la forme 
 ```{math}
:label:modulation
\varphi(t) = A(t) \cos(2\pi f_p(t) t + \phi(t))   
```
où  $A(t) $ représente l’**amplitude** du signal modulé, $ f_p (t)$ est la **fréquence porteuse** qui peut varier en temp, et  $ \phi(t)$ correspond à la **phase** du signal modulé.




Ci-dessous se trouve une explication de certains types de modulation: 
 

**1. Modulation d’amplitude analogique** (*Amplitude modulation - analog*)
- Le signal de message $ m(t) $ est **analogique**.
- L’amplitude de la porteuse $ A(t) $ varie en fonction de $ m(t) $.

**Types :**
-  Modulation à double bande latérale sans porteuse
**« DSB-SC : Double-sideband suppressed-carier »**
-  Modulation à double bande latérale
**« AM : Amplitude modulation »** 
-  Bande latérale unique
**« SSB : Single sideband »**
-  Modulation d'amplitude en quadrature (analogique)
**« QAM : Quadrature amplitude modulation»**



**2. Modulation d’angle analogique** (*Angle modulation - analog*)
Ce type de modulation concerne la phase ou la fréquence de la porteuse :
- Le signal de message $ m(t) $ est **analogique**.
- La phase $\phi(t) $ (ou la fréquence $ f_p(t)$) varie en fonction de  $m(t)$.

**Types :**
- Modulation de phase
**« PM : Phase modulation »** 
- Modulation de fréquence
**« FM : Frequency modulation »**




 **3. Modulation numérique**
Ce type de modulation s'applique aux signaux numériques :
- Le message $m(t)$ est **numérique** (valeurs discrètes, binaires ou multiniveaux).
- L’amplitude $A(t)$  **et/ou** la phase $ \phi(t)$ varient en fonction de $ m(t)$.

**Types :** 
- **« ASK : Amplitude Shift Keying »**  
- **« FSK : Frequency Shift Keying »**  
- **« PSK : Phase Shift Keying »** 
- **« QAM : Frequency Shift Keying »** 


 

 


###  Modulation d’amplitude (analogique) 

Les types de modulation d’amplitude analogique peuvent être classés en fonction de la manière dont l’information est transmise à travers l’onde porteuse. **La modulation à double bande latérale sans porteuse** (*Double-Sideband Suppressed-Carrier*; DSB-SC) supprime la composante continue de l’onde porteuse pour améliorer l’efficacité énergétique et spectrale. **La modulation à double bande latérale** (*Amplitude Modulation*; AM), quant à elle, transmet l’information en modulant l’amplitude d’une onde porteuse et en ajoutant une petite partie de la porteuse tout en deux bandes latérales. **La modulation à bande latérale unique** (*Single Sideband*; SSB) optimise encore plus l’utilisation du spectre en supprimant l’une des deux bandes latérales, réduisant ainsi la largeur de bande requise. Enfin, **la modulation d’amplitude en quadrature** (*Quadrature Amplitude Modulation*; QAM) combine deux signaux modulés en amplitude, déphasés de 90°, permettant ainsi une transmission plus efficace de l’information analogique avec une meilleure utilisation du spectre.  Les détails de ces types de modulations analogiques sont expliqués ci-dessous.

#### Modulation à double bande latérale porteuse supprimée (DSB-SC)

Modulation à double bande latérale porteuse supprimée (*double sideband suppressed carrier*; DSB-SC)  implique la multiplication du signal du message, ($m(t)$ limité à une bande de fréquence de $B$ Hz), une porteuse (onde sinusoïdale) de fréquence $ f_p $, notée $ c(t)= \cos(2\pi f_p t)$.

- **Modulation**  

Le signal modulé $ \varphi_{DSB-SC}(t)$ est donné par :
   $$
   \varphi_{DSB-SC}(t) = m(t) \cos(2\pi f_p t)
   $$
Ce signal ne contient plus la porteuse mais uniquement les bandes latérales.

En transformée de Fourier, le spectre du signal modulé est :
$$
 \Phi_{DSB-SC}(f) = \frac{1}{2} \left[ M(f + f_p) + M(f - f_p) \right]
$$
Cela montre que le spectre du signal est déplacé autour de $ \pm f_p $. 





```{figure} images/sec4-DSB-mod.png
:label: sec4-DSB-mod
:align: center 
Schéma de la modulation DSB-SC, où le signal $ m(t) $ est multiplié par une porteuse $ \cos(2\pi f_p t) $, déplaçant ainsi son spectre autour de $ \pm f_p $.
```




```{figure} images/sec4-envelope.png
:label: sec4-envelope
:align: center 
Une illustration de la modulation DSB-SC, où le signal $m(t) $ module la porteuse $\cos(2\pi f_p t)$ , pour générer  $\varphi_{DSB-SC}(t) = m(t) \cos(2\pi f_p t) $. 
```

 
- **Efficacité énergétique** 

 


L’efficacité énergétique est définie comme le rapport entre la puissance moyenne du signal message $ m(t) $ et celle du signal modulé $\varphi_{DSB-SC}(t) $. Dans le cas de la modulation **DSB-SC**, la puissance moyenne du signal modulé est :
$$
E[|\varphi_{DSB-SC}(t)|^2] = \frac{1}{2} E[|m(t)|^2]
$$

Donc, l’efficacité énergétique de la modulation DSB-SC est :
$$
\eta_{\text{efficacité-énergétique-DSB-SC}} = \frac{E[|m(t)|^2]}{E[|\varphi_{DSB-SC}(t)|^2]} = \frac{E[|m(t)|^2]}{\frac{1}{2} E[|m(t)|^2]} = 2
$$

Cela signifie que 50\% de la puissance du signal modulé est contenue dans le signal message $ m(t) $. La porteuse est supprimée (car il l y a pas une composante en $ f_p = 0 $), ce qui améliore l’efficacité énergétique du signal transmis. 

 

- **Efficacité spectrale**

Le spectre du signal modulé contient deux bandes latérales, ce qui double la largeur de bande du signal modulé par rapport au signal message, 
$$
\text{Largeur de bande de } \varphi_{DSB-SC}(t) = 2B
$$

Ainsi, l’efficacité spectrale de la modulation DSB-SC est :
$$
\eta_{\text{efficacité-spectrale-DSB-SC}} = \frac{B}{\text{Largeur de bande de } \varphi_{DSB-SC}(t)} = \frac{B}{2B} = \frac{1}{2}
$$

Cela signifie que seulement **50\%** de la largeur de bande du signal modulé est effectivement utilisée pour transmettre l’information.

```{figure} images/sec4-DSB-spectre.png
:label: sec4-DSB-spectre
:align: center 
L'image à gauche représente le spectre du signal de message $m(t)$. L'image à droite représente le spectre du signal après modulation DSB-SC. Les deux bandes latérales sont identiques et contiennent chacune la moitié de la puissance du signal d'origine, car   $ \Phi_{DSB-SC}(f) = \frac{1}{2} \left[ M(f + f_p) + M(f - f_p) \right]$.
 
```

- **Démodulation cohérente (synchrone)**


Le signal modulé reçu est filtré par un **filtre passe-bande**, qui réduit la puissance du bruit et ne laisse passer que les fréquences entre $ f_p - B $ et $ f_p + B $.  

Dans le cas idéal, Le filtre a une **réponse en fréquence** donnée par :
 $$
  H(f) =
  \begin{cases} 
  1, & f_p - B \leq |f| \leq f_p + B \\
  0, & \text{ailleurs}
  \end{cases}
$$

Le signal filtré est multiplié par une **porteuse locale** au récepteur :  
$$
  \cos(2\pi f_p t + \theta)
$$  
 La porteuse générée peut **ne pas être parfaitement alignée** avec celle de l'émetteur, ce qui introduit un décalage de phase $ \theta $ (**problème de synchronisation**).  

Après la multiplication avec la porteuse locale, le signal passe dans un **filtre passe-bas** avec une fréquence de coupure $ f_0 \geq B$, et gain de **2**, qui supprime les hautes fréquences et ne conserve que la composante basse fréquence du signal.   



```{figure} images/sec4-DSB-demod.png
:label: sec4-DSB-demod
:align: center 
Schéma de la démodulation cohérente d'un signal DSB-SC. Un filtre passe-bande réduit le bruit avant la multiplication avec une porteuse locale. Un filtre passe-bas extrait ensuite le signal message, avec un effet de synchronisation dépendant du décalage de phase $\theta$.
``` 
:::{warning} Effet de la synchronisation 
  - **Idéalement**, $ \theta = 0 $ et le signal récupéré est  exactement $ m(t)$.
  - **En pratique**, $ \theta \neq 0 $, ce qui entraîne une atténuation proportionnelle à $ \cos(\theta)  \leq 1 $.  
:::


 :::{tip} Synchronisation et Circuit PLL (*Phase Locked Loop*)
Le circuit PLL   est un système de synchronisation qui permet de verrouiller la phase d’un oscillateur sur celle d’un signal d’entrée.  
 

```{figure} images/sec4-pll.png
:label: sec4-pll
:align: center 
Schéma fonctionnel d’un circuit PLL utilisé pour la synchronisation des signaux.
``` 


Le signal d’entrée est mélangé avec le signal de l’oscillateur contrôlé en tension (*voltage controlled oscillator*; VCO).

Étapes de Traitement: 
- Point 1 : Signal d'entrée modulé $[A + m(t)]\cos(2\pi f_p t)$.
- Point 2 : Signal après le mixage, contenant une composante de haute fréquence $\frac{1}{2}[A + m(t)]\sin(4\pi f_p t)$.
- Point 3 :  Le signal résultant est filtré par un filtre passe-bas pour éliminer les hautes fréquences indésirables. En cas de syncronisation,  le signal est  nul après filtrage.
- Point 4 : Le signal filtré est ensuite utilisé pour ajuster la fréquence du VCO.  En cas de syncronisation, on observe le signal sinusoïdal $\sin(2\pi f_p t)$ après le VCO.
- Point 5 : Un déphaseur permet de générer un signal déphasé nécessaire à certaines applications. En cas de syncronisation, on observe le  signal cosinus $\cos(2\pi f_p t)$ après le déphaseur.
 
 :::




####  Modulation à double bande latérale (*Amplitude modulation*; AM)

- **Modulation**  

Le signal de message $m(t)$ et l'onde porteuse $ \cos(2\pi f_p t)$ sont combinés pour former :  
$$ 
\varphi_{AM}(t) = [A + m(t)] \cos(2\pi f_p t)
$$  
Le terme $ A $ est un gain choisi pour garantir que $ A + m(t) \geq 0 $, évitant ainsi toute **inversion de phase** (pour détecteur d’enveloppe).   




Le spectre du signal modulé est :
   $$
   \Phi_{AM}(f) = \frac{1}{2} \left[ M(f + f_p) + M(f - f_p) \right] +  \frac{A}{2} \left[ \delta(f + f_p) +\delta(f - f_p) \right] 
   $$
Cela montre que le spectre du signal est déplacé autour de $ \pm f_p $, et  contient une composante en fréquence $f_p$​ correspondant à la porteuse.

(def-SE)= 
Définition: Indice de modulation (*Modulation index*)
: **Indice de modulation**,  $ \mu $ est défini  par :  
 $$
     \mu = \frac{m_p}{A}
$$
Il représente le rapport entre l’amplitude maximale du signal message $ m_p $  et l’amplitude de la porteuse $ A $.  


```{figure} images/sec4-AM-mod.png
:label: sec4-AM-mod
:align: center 
Schéma du processus de modulation d’amplitude (AM), où le signal de message $m(t)$ module l’amplitude d’une porteuse $ \cos(2\pi f_p t)$ , en ajoutant un terme constant $A$ pour éviter toute inversion de phase.
```

```{figure} images/sec4-spectre-AM.png
:label: sec4-spectre-AM
:align: center 
Représentation fréquentielle du signal AM. Le spectre du signal de message $M(f)$, initialement centré autour de 0 Hz, est déplacé autour de $ \pm f_p $. ​ après modulation, incluant une composante $  f_p $. ​ correspondant à la porteuse et une largeur de bande totale de $2B$.
```








- **Efficacité énergétique** 


L'efficacité énergétique est définie comme le rapport entre la puissance moyenne du signal message $m(t)$et celle du signal modulé $\varphi_{AM}(t) $.  
$$
\eta_{\text{efficacité-énergétique-AM}} = \frac{E[|m(t)|^2]}{E[|\varphi_{AM}(t)|^2]}
$$

D'après la puissance moyenne du signal AM donnée :
$$
E[|\varphi_{AM}(t)|^2] = \frac{1}{2} A^2 + \frac{1}{2} E[|m(t)|^2]
$$

L'efficacité énergétique devient donc :
$$
\eta_{\text{efficacité-énergétique-AM}} = \frac{E[|m(t)|^2]}{\frac{1}{2} A^2 + \frac{1}{2} E[|m(t)|^2]}
$$

%En factorisant $ E[|m(t)|^2] $:
%$$
%\eta_{\text{efficacité-énergétique-AM}} = \frac{2 \mu^2}{1 + \mu^2}
%$$
%où $ \mu = \frac{m_p}{A} $ est l'indice de modulation.



:::{note} Exemple illustratif :  **Travail pratique - 4**
 
Un signal AM est observé à l'aide d'un analyseur de spectre avec une impédance d'entrée de  50Ω.  La porteuse a une fréquence de $f_p = 1 $ MHz, et les bandes latérales sont espacées de 2,5 kHz. L'affaiblissement des bandes latérales par rapport à la porteuse est de 12 dB.  

Déterminez l’indice de modulation $\mu $ du signal AM.  

```{figure} images/sec4-TP3.png
:label: sec4-TP3
:align: center 
Le spectre d’un signal AM. Notez que seules les fréquences positives sont visibles sur un oscilloscope.
```


**Réponse :**  On observe une différence de puissance de **12 dB** entre la porteuse et les bandes latérales. En utilisant la relation logarithmique entre ces puissances :
$$
12 \text{ dB} = 10 \log \left( \frac{4}{\mu^2} \right)
$$
En résolvant cette équation, on obtient :
$$
\mu= \frac{A_m}{A_p} = 0.5
$$

Pour TP4, nous calculons  le rendement, qui implique la quantité d'énergie du signal du message dans l'onde modulée divisée par l'énergie totale. Et il est obtenu comme suit :
$$
\textrm{Rendement} = \frac{2\mu^2}{4 + 2\mu^2}  = \frac{2(0.5)^2}{4 + 2(0.5)^2} = \frac{0.5}{4.5} \approx 11\%
$$ 
:::


- **Efficacité spectrale**

L'efficacité spectrale du signal AM est :
$$
\eta_{\text{efficacité-spectrale-AM}} = \frac{B}{2B} = \frac{1}{2}
$$
 


- **Démodulation non cohérente : Détecteur d’enveloppe** (*Envelope detector*)

 
L’**enveloppe** d’un signal AM représente l’amplitude instantanée du signal modulé. Pour un signal AM donné par :  
$$
\varphi_{AM}(t) = [A + m(t)] \cos(2\pi f_p t)
$$
l’enveloppe est définie par :  
$$
E(t) = A + m(t)
$$
Elle suit l’évolution du signal de message $ m(t) $, assurant ainsi que l’information est préservée dans la modulation.
Le **détecteur d’enveloppe** permet d’extraire cette enveloppe à partir du signal modulé. Il est généralement constitué de :
1.  Un redresseur (diode) qui élimine la partie négative du signal.
2.  Un circuit RC (résistance-capacité) qui agit comme un filtre passe-bas pour lisser les variations de la porteuse et récupérer l’enveloppe $ E(t)$.



```{figure} images/sec4-Env-circuit.png
:label: sec4-Env-circuit
:align: center 
Schéma d’un détecteur d’enveloppe utilisé pour la démodulation AM. Le circuit est composé d’une diode pour redresser le signal, d’un condensateur CC pour stocker la charge et d’une résistance RR qui détermine la constante de temps RC, permettant de lisser l’enveloppe du signal modulé.
```

 
```{figure} images/sec4-Env-RC.png
:label: sec4-Env-RC
:align: center 
Illustration du fonctionnement du détecteur d’enveloppe pour un signal AM. L’entrée du détecteur est un signal AM (courbe noire). La courbe bleue représente une extraction correcte de l’enveloppe. Une mauvaise constante de temps RC peut soit ralentir la détection (courbe rouge supérieure) soit causer une distorsion (courbe rouge inférieure).
```

 
Pour que le détecteur d'enveloppe fonctionne correctement, deux conditions doivent être respectées :  
1.  Il faut que **l’amplitude instantanée du signal modulé ne devienne jamais négative** pour éviter toute **inversion de phase**.  La condition mathématique est :  
  $$
     A + m(t) \geq 0, \quad \forall t
     $$
Cela impose que $    0 \leq \mu \leq 1$
 
2. La fréquence du signal message $ B $ doit être **beaucoup plus petite** que la fréquence porteuse $ f_p$ :  
$$
     B \ll f_p
$$
 Cela garantit que l’enveloppe varie lentement par rapport aux oscillations rapides de la porteuse.
 

:::{note} Exemple  illustratif :  **L'indice de modulation** et démodulation
Illustration de l'effet de l'indice de modulation $\mu $ en modulation d'amplitude (AM).
```{figure} images/sec4-mod-index.png
:label: sec4-mod-index
:align: center 
Chaque signal représente une onde modulée en amplitude pour différentes valeurs de $\mu $, allant de 0.2 à 1. Lorsque $\mu $ augmente, l'amplitude de l'onde modulée varie davantage, influençant l'enveloppe du signal. À $\mu = 1 $, l'enveloppe atteint zéro à certains instants, ce qui correspond à une modulation à $100\%$.
```

 

La **surmodulation** (*overmodulation*) en modulation d'amplitude (AM) se produit lorsque $\mu > 1 $. Cela signifie que l'amplitude du signal message $ m(t) $ devient supérieure à celle de la porteuse$ A $, entraînant une **inversion de phase** dans l'onde modulée.  

Ce phénomène provoque une distorsion du signal, rendant difficile voire impossible sa démodulation correcte, en particulier avec un démodulateur à enveloppe. Pour éviter la surmodulation et assurer une transmission fidèle du signal, il est recommandé de maintenir $\mu \leq 1 $.


```{figure} images/sec4-surmodulation.png
:label: sec4-surmodulation
:align: center 
Illustration de la surmodulation $ \mu = 1.5 $ en modulation d'amplitude (AM). Lorsque l'indice de modulation dépasse 1, l'enveloppe du signal devient déformée et présente des **inversions de phase**, ce qui entraîne des distorsions non désirées et rend la démodulation plus complexe.  
```
:::


 
 

- **Démodulation cohérente (synchrone)**


```{figure} images/sec4-AM-Demod-Coh.png
:label: sec4-AM-Demod-Coh
:align: center 
Schéma d’un démodulateur cohérente  La figure illustre le principe de la  démodulation cohérente d'un signal AM en utilisant une  PLL (*phase locked  loop*). Cette méthode permet de récupérer avec précision le signal de message $ m(t)$ à partir du signal modulé, en synchronisant une porteuse locale avec celle du signal reçu.
```



Le signal modulé en entrée est donné par $ \varphi_{AM}(t) = [A + m(t)] \cos(2\pi f_p t) $. L'objectif est d'extraire uniquement $ m(t) $en éliminant la porteuse. Pour cela, le signal entre d’abord dans un **mélangeur** (*mixer*), qui effectue une multiplication avec un signal de référence $ \cos(2\pi f_p t) $. Cette opération produit deux termes : une **composante basse fréquence** correspondant à l’enveloppe $ A + m(t) $ et une **composante haute fréquence** centrée autour de $ 2f_p $.



Pour isoler le signal utile, un **filtre passe-bas** est appliqué après le mélangeur. Ce filtre élimine les hautes fréquences et ne conserve que la composante basse fréquence, soit $ A + m(t) $. Notez que, à  ce stade, bien que l’information du message soit récupérée, une erreur de phase pourrait perturber la démodulation si la porteuse locale utilisée dans le mélangeur n’est pas parfaitement synchronisée avec celle du signal reçu.

C’est à ce niveau qu’intervient la PLL (*Phase Lock Loop*). Ce circuit ajuste dynamiquement la fréquence et la phase de la porteuse locale pour s’assurer qu’elle est **en parfaite synchronisation** avec la porteuse du signal reçu. En maintenant cet alignement, la PLL permet d’éviter les erreurs de phase qui pourraient altérer la restitution du signal de message.

Finalement, à la sortie du filtre, on obtient $ A + m(t)$ , qui peut être traité pour supprimer la constante $  A $ , généralement via un **filtre passe-haut**. Cette dernière étape permet d’obtenir uniquement le signal $  m(t)$ , qui est la réplique exacte du signal de message initialement modulé à l’émission. Ainsi, grâce à cette méthode cohérente, la démodulation est réalisée avec une précision élevée, rendant cette approche particulièrement utile dans les communications nécessitant une forte immunité aux distorsions et aux interférences.


:::{important} Exemple pratique : 

```{figure} images/Sec4-RadioAM.png
:label: Sec4-RadioAM
:align: center 
Évolution de la bande de fréquences AM au Québec et au Canada. La bande AM, initialement comprise entre **535 kHz et 1605 kHz**, a été étendue jusqu'à **1705 kHz**, passant de 107 à 117 canaux de **10 kHz** chacun. Cette extension permet d’accueillir de nouvelles stations et d’améliorer la répartition des fréquences pour la radiodiffusion.
```

 
 
Auparavant, la bande AM était définie entre **535 kHz et 1605 kHz**, divisée en **107 canaux de 10 kHz** chacun. Actuellement, cette bande a été étendue jusqu'à **1705 kHz**, offrant désormais **117 canaux de 10 kHz**. Cette extension permet d’accueillir davantage de stations de radio et d’améliorer la disponibilité des fréquences pour la diffusion. 

L’illustration montre également une **représentation spectrale d’une station de radio AM**, où l’espacement entre les canaux est de **10 kHz**, ce qui correspond à la largeur de bande attribuée à chaque station. Étant donné que les signaux AM transmettent des fréquences audio allant jusqu'à **5 kHz**, chaque station doit occuper une bande de **10 kHz** (incluant la bande latérale supérieure et inférieure). 

Une indication est également donnée concernant l’**extension récente** de la bande AM, qui s’est élargie de **1605 kHz à 1705 kHz** pour accueillir des fréquences supplémentaires. Enfin, la figure précise que ces fréquences sont les mêmes aux **États-Unis**, soulignant une harmonisation des bandes de radiodiffusion en Amérique du Nord.
:::




Modulations efficaces du point au vue de la largeur de bande sont la Modulation à bande latérale unique (*single sideband*; SSB) et la modulation d'amplitude en quadrature (analogique)  (*quadrature amplitude modulation - analog*; QAM-Analogique). Elles sont décrites ci-dessous.  


####  Modulation à bande latérale unique (SSB)

 Dans une modulation AM classique, l’information transmise est redondante, car elle est contenue à la fois dans la **bande latérale supérieure** et la **bande latérale inférieure**. Il est donc possible d’envoyer le même message en utilisant **seulement une des deux bandes**, réduisant ainsi de moitié la largeur de bande nécessaire. 

 - **Modulation**  
```{figure} images/sec4-ssb-mod.png
:label: sec4-ssb-mod
:align: center 
 Illustration de la génération d’un signal **SSB (Single Sideband)** en utilisant la **méthode par déphasage**, qui permet de supprimer l’une des bandes latérales.
```
 



On utilise deux branches pour générer un signal modulé de SSB. Dans la **première branche**, $m(t)$ est directement multiplié par la porteuse  $\cos(2\pi f_p t)$ pour obtenir 
$$
  s_1(t) = m(t) \cos(2\pi f_p t)
$$
 Dans la **deuxième branche**, le signal est d'abord transformé par un **filtre à déphasage** $ H(f)$, qui effectue un décalage de phase de  $ \frac{\pi}{2} $ (Transformée de Hilbert):
  $$
  s_2(t) = \hat{m}(t) = H(f) \cdot M(f) \quad \text{où} \quad H(f) = je^{-j\pi u(f)}
  $$
  Ce signal est ensuite multiplié par une **porteuse en quadrature** $ \sin(2\pi f_p t) $ :
  $$
  s_3(t) = \hat{m}(t) \sin(2\pi f_p t)
  $$

```{figure} images/sec4-hilbert.png
:label: sec4-hilbert
:align: center 
Représentation fréquentielle du filtre de Hilbert (déphasage) : la phase $\angle H(f) $ introduit un déphasage de $ \frac{\pi}{2} $  pour les fréquences positives et de $ -\frac{\pi}{2} $ pour les fréquences négatives, tandis que le module $|H(f)| $ reste constant à 1.
```


Finalement, les deux signaux obtenus sont combinés. Pour générer la **bande latérale supérieure** (*upper sideband*; USB), on effectue une addition :
$$
  \varphi_{SSB}^{USB}(t) = s_1(t) + s_3(t) = m(t) \cos(2\pi f_p t) + \hat{m}(t) \sin(2\pi f_p t)
$$
Pour générer la **bande latérale inférieure** (*lower sideband*; LSB ), on effectue une soustraction :
$$
  \varphi_{SSB}^{LSB}(t) = s_1(t) - s_3(t) = m(t) \cos(2\pi f_p t) - \hat{m}(t) \sin(2\pi f_p t)
$$

L’expression en fréquence du signal SSB est obtenue en utilisant la transformée de Fourier :
- Pour la **USB**, le spectre est :
  $$
  \Phi_{SSB}^{USB}(f) = M(f - f_p) u(f - f_p)
  $$
- Pour la **BLI**, le spectre est :
  $$
  \Phi_{SSB}^{LSB}(f) = M(f + f_p) u(-f - f_p)
  $$


Grâce à cette approche, seule **une des bandes latérales est transmise**, ce qui permet de réduire **de moitié la largeur de bande** par rapport à une modulation AM conventionnelle. Cette technique est particulièrement utilisée dans les communications à bande limitée, comme la radio HF et certains systèmes de télécommunications analogiques avancés.




```{figure} images/sec4-ssb-spectre.png
:label: sec4-ssb-spectre
:align: center 
Représentation spectrale des différentes techniques de modulation en amplitude : (1) Signal modulant en bande de base, (2) Modulation à double bande latérale (DSB), (3) Modulation à bande latérale unique supérieure (SSB-USB), et (4) Modulation à bande latérale unique inférieure (SSB-LSB). La modulation SSB permet de réduire la largeur de bande nécessaire en ne transmettant qu'une seule bande latérale du spectre du signal modulé.
```



- **Efficacité énergétique** 

Pour SSB (modulation à bande latérale unique) efficacité énergétique est
     $$
     \eta_{\text{efficacité-énergétique-SSB}}^{SSB} = 1
     $$

- **Efficacité spectrale**  
La largeur de bande occupée est **\( B \)**, donc :
$$
     \eta_{\text{efficacité-spectrale-SSB}} = \frac{B}{B} = 1
$$

 

- **Démodulation cohérente (synchrone)**

```{figure} images/sec4-ssb-demod.png
:label: sec4-ssb-demod
:align: center 
Démodulation d'un signal à bande latérale unique avec une erreur de phase dans l'oscillateur local. Un filtre passe-bas est utilisé pour récupérer le signal modulant, mais une erreur de phase $ \theta $ peut causer une distorsion du signal démodulé.
```

 Signal d'entrée est $ \varphi_{SSB}(t)$ est le signal modulé en bande latérale unique qui arrive au récepteur. Il est multiplié par une porteuse locale $\cos(2\pi f_p t + \theta) $, où $\theta$  représente une erreur de phase potentielle 
$$
   x(t) = \varphi_{SSB}(t) \cos(2\pi f_p t + \theta)
$$

Le signal obtenu après multiplication (*mixing*) est noté $x(t) $, et il peut contenir des composantes en bande de base ainsi que du bruit. Un filtre passe-bas $H(f)$ est appliqué pour éliminer les composantes haute fréquence indésirables, conservant uniquement le signal souhaité, 
$$
v(t) = H(f) * x(t)
$$

Finalement, $ v(t)$ est le signal démodulé en bande de base, qui peut être affecté par l’erreur de phase $ \theta $, entraînant une distorsion du message.


####  Modulation d'amplitude en quadrature (analogique)  (QAM-Analogique)

La modulation d’amplitude en quadrature (QAM-Analogique),  permet la transmission simultanée de deux signaux distincts $m_1(t)$ et $m_2(t)$ en utilisant une onde  porteuses  avec deux phases (*inphase* et *quadrature*).

-  **Modulation**   

 
Nous avons **deux signaux messages** distincts, $ m_1(t)$ et $ m_2(t) $, chacun d'eux possède une largeur de bande de $ B $ Hz.  Dans le cas d'une modulation en quadrature (QAM), ces deux signaux peuvent être transmis **simultanément** en les associant à des porteuses orthogonales, comme un cosinus et un sinus à une fréquence porteuse $ f_p $. L’utilisation de deux signaux de largeur de bande $ B $ permet d’augmenter l’utilisation du spectre tout en assurant une séparation correcte des informations transmises.

 ```{figure} images/sec4-qam-mod.png
:label: sec4-qam-mod
:align: center 
La modulation d’amplitude en quadrature (QAM-Analogique) permettant la transmission simultanée de deux signaux $m_1(t)$ et $m_2(t) $ grâce à l'utilisation de deux porteuses orthogonales en cosinus et en sinus avec $f_p$.
```

Le signal $ m_1(t)$ module une porteuse en cosinus :   
$$
c_1(t) = \cos(2\pi f_p t)
$$
Le signal après le multiplexage est  :  
$$
m_1(t) \cos(2\pi f_p t)
$$

Dans la deuxième branche, le signal $m_2(t)$ module une porteuse en sinus, obtenue par un déphasage de $ -\pi/2 $ :  
$$
     c_2(t) = \sin(2\pi f_p t)
$$
Le signal après le multiplexage avec $ c_2(t)$  est :  
$$
     m_2(t) \sin(2\pi f_p t)
$$


La somme des deux signaux forme le signal QAM-A :  
$$
     \varphi_{QAM-A}(t) = m_1(t) \cos(2\pi f_p t) + m_2(t) \sin(2\pi f_p t)
$$



- **Efficacité énergétique** 
 
Dans le cas de la modulation QAM-A avec deux signaux $m_1(t)$ et $m_2(t)$,   l’efficacité énergétique est :
$$
\eta_{\text{efficacité-énergétique-QAM}} = \frac{E[|m_1(t)|^2] + E[|m_2(t)|^2]}{E[|\varphi_{\text{QAM}}(t)|^2] }  
$$
Supposons que les deux signaux $m_1(t)$ et $m_2(t)$ ont la même puissance,

$$
\eta_{\text{efficacité-énergétique-QAM-A}} = 1 
$$ 
 

- **Efficacité spectrale**

Pour la modulation QAM-A, la largeur de bande du signal modulé est  égale à celle du message $B$, car chaque signal $ m_1(t) $ et $m_2(t) $ occupe la même bande de fréquence, et l'orthogonalité des porteuses permet d'éviter l'élargissement du spectre, donc
$$
\eta_{\text{efficacité-spectrale-QAM-A}} = \frac{B}{B} = 1
$$

  




- **Démodulation cohérente (synchrone)**

```{figure} images/sec4-qam-demod.png
:label: sec4-qam-demod
:align: center 
 Démodulation cohérente de la QAM : séparation des signaux $m_1(t) $ et $ m_2(t) $ en utilisant des porteuses en quadrature et un filtrage passe-bas.
```


La démodulation cohérente de la QAM-A consiste à extraire les deux signaux modulants $ m_1(t) $ et $m_2(t) $ en utilisant des signaux de référence synchrones. Ce procédé repose sur le produit du signal reçu $ \varphi_{\text{QAM-A}}(t)$ avec les mêmes porteuses utilisées lors de la modulation, suivi d’un filtrage passe-bas.

Le signal reçu est
 $$   \varphi_{\text{QAM-A}}(t) = m_1(t) \cos(2\pi f_p t) + m_2(t) \sin(2\pi f_p t)
   $$

Multiplication avec $ c_1(t) = \cos(2\pi f_p t) $ donne
$$
   s_2(t) = \varphi_{\text{QAM-A}}(t) \cos(2\pi f_p t) = m_1(t) \cos^2(2\pi f_p t) + m_2(t) \sin(2\pi f_p t) \cos(2\pi f_p t) 
$$

Après filtrage passe-bas, gain de 2,  on obtient
$$
   s_3(t) =  m_1(t)
$$


En plus, la multiplication avec $c_2(t) = \sin(2\pi f_p t) $  
$$
   s_3(t) = \varphi_{\text{QAM-A}}(t) \sin(2\pi f_p t) = m_1(t) \cos(2\pi f_p t) \sin(2\pi f_p t) + m_2(t) \sin^2(2\pi f_p t)
$$
  et après filtrage passe-bas (gain de 2) on a 
$$
   s_5(t) =  m_2(t)
$$

 
Donc chaque signal modulant est extrait grâce aux signaux de référence synchrones et au filtrage passe-bas qui supprime les fréquences élevées. Notez que cette méthode nécessite une parfaite synchronisation pour éviter les interférences entre les deux canaux.

 

%```{figure} images/sec4-DSB-SC.png
%:label: sec4-message
%:align: center 
%Aciklama
%```








%### **Propriétés clés de la démodulation cohérente :**  
%- **Nécessite une synchronisation précise** entre l’émetteur et le récepteur.  
%- **Un mauvais alignement de phase (\( \theta \)) cause une perte d’amplitude**, voire une distorsion du signal récupéré.  
%- **Utilisée dans les systèmes de communication nécessitant une récupération fidèle du signal message** (radio, télévision, télécommunications numériques).

%---



:::{tip}  Conversion de fréquence 
 La conversion de fréquence est un processus fondamental dans les récepteurs radio et les systèmes de communication. Elle permet de transférer un signal d’une fréquence radioélectrique (RF) à une fréquence intermédiaire (*intermediate frequency*; IF), facilitant ainsi le traitement du signal. Cette conversion est réalisée à l’aide d’un mélangeur, qui combine le signal RF avec un signal d’oscillateur local (LO) pour produire des composantes de fréquence somme et différence.
```{figure} images/sec4-IF.png
:label: sec4-IF
:align: center 
Processus de conversion de fréquence et filtrage des signaux RF et IF.
```


Le signal modulé est centré autour de la fréquence $f_p$. Un filtre RF (bande passante) est appliqué pour sélectionner la bande de fréquence désirée et atténuer les interférences et le bruit.  Une fréquence d’image $f_{\text{IMAGE}}$ peut apparaître symétriquement autour de l’oscillateur local et doit être éliminée.
 

 Un oscillateur local de fréquence $f_0$ est utilisé pour mixer le signal RF. Deux nouvelles fréquences sont produites :
 -  $f_{\text{IF}} = |f_p - f_0|$ (fréquence intermédiaire)
 - $f_{\text{IMAGE}} = |f_{\text{IMAGE}} - f_0|$
    
Notez que la fréquence d’image peut interférer avec le signal souhaité si elle n’est pas correctement filtrée. 

Après le mixage, le signal est déplacé à une fréquence intermédiaire $f_{\text{IF}}$. Un filtre IF est appliqué pour sélectionner uniquement la bande souhaitée et rejeter les fréquences parasites, y compris l’image.
 
La conversion de fréquence est une technique essentielle dans les récepteurs radio et les systèmes de télécommunications. Elle permet de déplacer un signal d’une fréquence élevée à une fréquence intermédiaire où il est plus facile à traiter, tout en réduisant les interférences et le bruit.
:::
 

:::{tip}  Récepteur Superhétérodyne 

La conversion de fréquence et l’architecture superhétérodyne sont des concepts fondamentaux dans les récepteurs radio et les systèmes de communication modernes. La conversion de fréquence permet de déplacer un signal d’une fréquence RF (radiofréquence) à une fréquence IF (intermédiaire) pour un traitement plus efficace. L'architecture superhétérodyne repose sur ce principe et a évolué au fil du temps, notamment avec l'avènement des technologies numériques.

```{figure} images/sec4-suphet.png
:label: sec4-suphet
:align: center 
Évolution du récepteur superhétérodyne vers une architecture entièrement numérique.
```
:::

 
 




### Modulation d’angle (analogique) 
La modulation d’angle est une technique de modulation dans laquelle l’angle de la porteuse est modifié en fonction du signal message, comme noté dans [](#modulation). Elle inclut deux types principaux :

- Modulation de fréquence (FM)   où la fréquence instantanée varie proportionnellement au signal modulant.
- Modulation de phase (PM)   où la phase de la porteuse est directement influencée par le signal modulant.


  Nous avons besoin de la notion de fréquence instantanée pour pouvoir définir les types de modulation d’angle.



(def-IF)= 
Définition: Fréquence instantanée (*instantaneous frequency*)
: Considerons un signal modulé, $\varphi(t)=A \cos(\phi(t))$, la **fréquence instantanée** d'un signal modulé est donnée par :
\begin{equation}
    f_i(t) = \frac{1}{2\pi} \frac{d\phi(t)}{dt}
\end{equation}
où $\phi(t)$ représente la phase du signal modulé.

 
#### Modulation de Fréquence (*Frequency modulation*; FM)
Dans la modulation de fréquence, l'expression du signal modulé est donnée par :
$$
    \varphi_{FM}(t) = A \cos \left( 2\pi f_p t + 2\pi k_f \int_0^t m(\tau) d\tau \right)
$$
où $A$ est l’amplitude du signal modulé, $f_p$ est la fréquence porteuse, $k_f$ est le coefficient de sensibilité en fréquence [Hz/V], $m(t)$ est le signal modulant (signal de message).

La **fréquence instantanée** du signal modulé est définie par :
$$
    f_i(t) = f_p + k_f m(t)
$$

La **déviation maximale de fréquence** est donnée par :
 $$
    \Delta f = k_f |m(t)|_{MAX}
$$
 
#### Modulation de Phase  (*Phase modulation*; PM)
Dans la modulation de phase, l'expression du signal modulé s’écrit :
 $$
    \varphi_{PM}(t) = A \cos \left( 2\pi f_p t + 2\pi k_p m(t) \right)
 $$
où $k_p$ est le coefficient de sensibilité en phase.

La **fréquence instantanée** est :
 $$
    f_i(t) = f_p + k_p \frac{d m(t)}{dt}
 $$

La **déviation de fréquence maximale** est alors donnée par :
 $$
    \Delta f = k_p \left| \frac{d m(t)}{dt} \right|_{MAX}
 $$

:::{warning} Attention

 - En **FM**, la fréquence instantanée varie en fonction de l’amplitude de $m(t)$.
 - En **PM**, la fréquence instantanée dépend de la dérivée du signal modulant $m(t)$.

```{figure} images/sec4-fm-pm.png
:label: sec4-fm-pm
:align: center 
Illustration des modulations d’angle : une porteuse (en bleu), un signal modulant (en vert), et les signaux résultants en modulation de fréquence (FM, en rouge) et en modulation de phase (PM, en cyan).
```
:::

  
  
####  **Analyse Spectrale de la FM** 

L'analyse spectrale de la modulation de fréquence (FM) est essentielle pour comprendre la répartition de l'énergie du signal modulé en fréquence.  Tout d'abord, définissons la fonction de Bessel. 

:::{tip} La fonction de Bessel
La fonction de Bessel d’ordre $n$ est définie par :
$$
    J_n(\beta) = \frac{1}{\pi} \int_0^\pi \cos(n\theta - \beta \sin(\theta)) d\theta
$$
et peut être exprimée sous une autre forme en série infinie :
$$
    J_n(\beta) = \sum_{k=0}^{\infty} \frac{(-1)^k (\beta/2)^{2k+n}}{k! (k+n)!}
$$

Les valeurs de $J_n(\beta)$ déterminent **l’amplitude** des différentes composantes fréquentielles de la FM. 


```{figure} images/sec4-bessel.png
:label: sec4-bessel.png
:align: center 
Représentation des fonctions de Bessel de première espèce $J_n​(x)$ pour différents ordres $n$.
```
:::



Soit un signal modulant sinusoïdal :
$$
    m(t) = A_m \cos(2\pi f_m t)
$$

Le signal FM correspondant est donné par :
$$
    \varphi_{FM}(t) = A \cos(2\pi f_p t + \beta \sin(2\pi f_m t))
$$
où  $f_p$ est la fréquence porteuse, $f_m$ est la fréquence du signal modulant, et  $\beta$ est l’indice de modulation.
 
L'équation du signal FM peut être exprimée sous forme de série de **Bessel** :
```{math}
:label:FM-time
    \varphi_{FM}(t) = A \sum_{n=-\infty}^{\infty} J_n(\beta) \cos(2\pi [f_p + n f_m] t)
```
Cela montre que le spectre FM est composé d'un **ensemble de fréquences discrètes**, situées à :
$$
    f_p + n f_m
$$
avec des amplitudes pondérées par les **fonctions de Bessel** $J_n(\beta)$.

La densité spectrale du signal FM est obtenue par :
```{math}
:label:spectre-FM
    \Phi_{FM}(f) = \frac{A}{2} \sum_{n=-\infty}^{\infty} J_n(\beta) \left\{ \delta(f + [f_p + n f_m]) + \delta(f - [f_p + n f_m]) \right\}
```
Cette équation signifie que l’énergie du signal est répartie sur **plusieurs raies spectrales** au lieu d’être concentrée sur une seule fréquence.

```{figure} images/sec4-fm-spectre.png
:label: sec4-fm-spectre.png
:align: center 
Spectre du signal FM de  [](#spectre-FM). raies spectrales situées aux fréquences $ f_p + n f_m $, avec des amplitudes pondérées par les fonctions de Bessel $ J_n(\beta) $
```

L’illustration montre les **composantes spectrales** aux différentes fréquences multiples de $f_m$, avec des amplitudes proportionnelles aux **valeurs des fonctions de Bessel** $J_n(\beta)$. Cette analyse est essentielle pour la conception de **systèmes de communication FM** et pour comprendre leur occupation spectrale. Notez que la bande passante théorique des signaux FM est **infinie**; cependant, elle est approximée selon la règle de Carson ci-dessous.
 


 

-**Règle de Carson**

La règle de Carson fournit une estimation pratique de la bande passante des signaux FM et PM en fonction de l’indice de modulation $\beta$, évitant ainsi l'hypothèse d'une bande passante infinie.
 
  
Pour la **modulation de fréquence (FM)**, la bande passante est donnée par :
$$
 B_{FM} = 2B (\beta + 1) \quad \text{Hz}
$$
où l'indice de modulation $\beta$ est défini comme :
$$
    \beta = \frac{\Delta f}{B}, \quad \Delta f = k_f \frac{m_{max} - m_{min}}{2 \times 2\pi}
$$
 
Pour la **modulation de phase (PM)**, la bande passante suit une expression similaire :
$$
    B_{PM} = 2B (\beta + 1) \quad \text{Hz}
$$
avec :
$$
    \beta = \frac{\Delta f}{B}, \quad \Delta f = k_p \frac{|m(t)|_{max} - |m(t)|_{min}}{2 \times 2\pi}
$$


- **Démodulation d’un Signal FM**

```{figure} images/sec4-FM-demod.png
:label: sec4-FM-demod 
:align: center 
Démodulation d’un signal FM par détection d’enveloppe après dérivation
```


 
La démodulation de la FM repose sur l’extraction du signal modulant $ m(t) $ à partir du signal reçu. Une approche classique consiste à utiliser un détecteur basé sur la dérivation suivie d’une détection d’enveloppe. 
 
Un signal modulé en fréquence s’écrit sous la forme :
$$
    \varphi_{FM}(t) = A \cos \left( 2\pi f_p t + 2\pi k_f \int_{-\infty}^{t} m(\alpha) d\alpha \right)
$$
où $f_p $ est la fréquence porteuse et $ k_f $ représente le coefficient de sensibilité en fréquence.
 
La dérivée du signal FM est donnée par :
$$
    \frac{d\varphi_{FM}(t)}{dt} = -A(2\pi f_p + 2\pi k_f m(t)) \sin \left( 2\pi f_p t + 2\pi k_f \int_{-\infty}^{t} m(\alpha) d\alpha \right)
$$
Cette expression met en évidence que l’amplitude de la fonction sinus est proportionnelle à la fréquence instantanée du signal.

Le processus de démodulation ppour la FM suit les étapes suivantes :

- **Dérivation** : L’application d’un dérivateur permet de transformer les variations de fréquence en variations d’amplitude. L’amplitude de la sortie est proportionnelle à la fréquence instantanée :
    $$
        |A(2\pi f_p + 2\pi k_f m(t))|
   $$

- **Détection d’enveloppe** :  L’amplitude extraite par le dérivateur est ensuite récupérée à l’aide d’un détecteur d’enveloppe qui permet de retrouver le signal modulant $ m(t) $.



:::{note} Exemple  illustratif : 


```{figure} images/sec4-FM-demod-ex.png
:label: sec4-FM-demod-ex.png
:align: center 
Un signal FM et de sa dérivée pour la démodulation
```
La démodulation d’un signal FM par différentiation et détection d’enveloppe exploite la relation entre la fréquence instantanée du signal reçu et l’amplitude du signal différentié. Cette technique est largement utilisée dans les récepteurs FM analogiques en raison de sa simplicité de mise en œuvre.

:::



:::{tip} Le multiplexage  fréquentiel
Le multiplexage  fréquentiel  (*Frequency Division Multiplexing*; FDM) est une technique qui permet de transmettre plusieurs signaux simultanément sur un même canal en les modulant sur des fréquences porteuses distinctes. 
Le FDM est une technique essentielle dans les systèmes de communication modernes, notamment pour les transmissions analogiques et numériques, comme la  FM, la télévision et les réseaux de télécommunications.

```{figure} images/sec4-fdm.png
:label: sec4-fdm.png
:align: center 
Principe du multiplexage fréquentiel : transmission simultanée de plusieurs signaux sur un seul canal par attribution de bandes de fréquences distinctes.
```

Soit $m_1(t), m_2(t), ..., m_N(t)$ plusieurs signaux avec une largeur de bande de $B$ Hz.    Chaque signal est modulé sur une fréquence porteuse distincte $f_1, f_2, ..., f_N$ en utilisant une modulation d’amplitude ou de fréquence.  Les signaux modulés sont ensuite combinés (sommation) pour être transmis sur un seul canal.
 
 Le signal composite est transmis à travers un canal unique contenant toutes les composantes fréquentielles modulées. À la réception, des filtres passe-bande sont appliqués pour extraire chaque signal modulé individuellement.
  Chaque signal est ensuite démodulé à l’aide d’un oscillateur local afin de retrouver son contenu d’origine $m_1(t), m_2(t), ..., m_N(t)$.
  :::
 




:::{important} Exemple pratique : 
```{figure} images/sec4-radio-fm.png
:label: sec4-radio-fm.png
:align: center 
Bande FM au Canada : répartition des fréquences et interaction avec la télévision
```
 Au Québec et au Canada, la bande FM est définie par des fréquences comprises entre 88 MHz et 108 MHz, comme illustré dans la figure. La bande FM est subdivisée en 100 canaux, chacun ayant une largeur de bande de 200 kHz. Cette séparation permet aux stations de radio d’émettre sans interférences majeures entre elles.
Les fréquences allouées aux stations de radio augmentent de 200 kHz en 200 kHz, à partir de 88 MHz jusqu’à 108 MHz.


Dans la figure, il est aussi montré que le canal 6 de la télévision analogique chevauche en partie la bande FM. Plus précisément, le signal sonore associé à ce canal est transmis en FM sur une fréquence porteuse de 87,75 MHz. Cette fréquence se trouve juste avant le début officiel de la bande FM (88 MHz), ce qui explique pourquoi certaines radios peuvent capter ce signal télévisuel sur la bande FM.
:::


 





%- La modulation FM génère un spectre composé de plusieurs raies fréquentielles au lieu d'une seule fréquence centrale.
%- Les amplitudes des différentes composantes sont déterminées par les fonctions de Bessel.
%- Plus l’indice de modulation $\beta$ est élevé, plus le spectre est large, ce qui explique pourquoi la FM utilise plus de bande passante que l’AM.
 


 




## Modulation numérique  

La modulation numérique peut être utilisée lorsque la source est numérique. Elle permet de convertir une séquence de bits en un signal modulé adapté à la transmission sur un canal de communication.
Nous pouvons également utiliser la modulation numérique à la sortie d’un modulateur par impulsions codées (PCM). 

Dans un système de communication numérique, le flux de bits représente une séquence temporelle de valeurs binaires ($\texttt{0}$ et $\texttt{1}$) qui doit être convertie en un signal physique pour la transmission. Ce flux peut être exprimé sous forme mathématique en utilisant une somme de fonctions impulsionnelles centrées sur les instants de temps où chaque bit est transmis.
Le signal correspondant au flux de bits peut être modélisé comme :
$$
b(t) = \sum_{k} b_k \delta (t - kT_b)
$$
où  $b_k$ est la valeur du $ k$-ième bit, appartenant à l’ensemble $\{\texttt{0},\texttt{1}\}$,  $T_b$ est la  période de bit (l’intervalle de temps entre deux bits consécutifs),
et finalement $\delta(t)$ est l'impulsion de Dirac, utilisée pour représenter un signal discret en un ensemble d’impulsions temporelles.

### Modulation numérique sans porteuse  
Nous commencerons la discussion par la transmission binaire, qui permet de générer deux symboles distincts. Pour utiliser la modulation numérique, il est indispensable d’employer un codeur de symboles. 
Dans le cas binaire, cela implique deux symboles distincts. Nous représenterons le nombre de symboles par $M$. 

(def-Modulation)=
Définition: Codeur de symboles
: Un **codeur de symboles** regroupe les bits ($\texttt{0}$ ou $\texttt{1}$) en séquences appelées **symboles** (en Volts), où chaque symbole peut représenter un ou plusieurs bits en fonction du schéma de modulation utilisé.
```{figure} images/sec4-BinSymCod.png
:label: sec4-BinSymCod.png
:align: center 
Le schéma représente un codeur de symboles qui transforme une séquence binaire en symboles ($M=2$).
L'entrée du codeur est une séquence de bits $b_k$, $b(t)$ qui est ensuite transformée en un ensemble de signal de sortie $s(t)$, correspondant à des symboles spécifiques utilisés pour la transmission. Ce processus est essentiel dans les systèmes de communication numérique pour adapter les données binaires à un format compatible avec une modulation spécifique.
```

:::{note} Exemple illustratif : 

Cet exemple illustre la conversion d’un bit d’entrée binaire en un symbole de sortie sous forme de tension. 

```{list-table}
:header-rows: 1

* - $b_k$ (Bit d'entrée [Binaire])
  - $s_k$ (Symbole de sortie [Tension])
* - $\texttt{1}$
  - 5V
* - $\texttt{0}$
  - 0V
```

Lorsqu’un bit d’entrée $\texttt{1}$ est reçu, la sortie correspondante est une tension de 5V, tandis que lorsqu’un bit d’entrée $\texttt{0}$ est reçu, la sortie est 0V.  

```{figure} images/sec4-bits.png
:label: sec4-bits.png
:align: center 

Représentation du signal $b(t)$, correspondant à la séquence binaire d’entrée où chaque bit est maintenu pendant une durée $T_b$ = 1 seconds
```

```{figure} images/sec4-symbols.png
:label: sec4-symbols.png
:align: center 

Représentation du signal $b(t)$, correspondant à la séquence binaire d’entrée où chaque bit est maintenu pendant une durée $T_b$ = 1 seconds
```

:::


 


Pour les codeurs de symboles **binaires** ($M=2$), le signal de sortie, composé de symboles toutes les $T_b$​ secondes, peut s'écrire comme
\begin{equation}
s(t) = \sum_{k} s_k \delta (t - kT_b)
\end{equation}


####  2-PAM « Binary Pulse Amplitude Modulation »

La modulation d’amplitude par impulsions binaire (*Binary Pulse Amplitude Modulation* ; 2-PAM) est une technique de Modulation numérique  binaire   sans porteuse  dans laquelle l’amplitude d’une impulsion est modulée en fonction d’un signal binaire. Cela signifie que les symboles transmis ne prennent que **deux niveaux distincts**, généralement associés aux bits $\texttt{0}$ et $\texttt{1}$.



Le signal modulé en **2-PAM** peut être exprimé comme suit :
$$
\varphi_{2-PAM}(t) = s(t) * p(t) = \sum_{k} s_k p(t - kT_b)
$$ 
où le codeur de symboles est
```{list-table}
:header-rows: 1
* - $b_k$ (Bit d'entrée [Binaire])
  - $s_k$ (Symbole de sortie [Tension])
* - $\texttt{1}$
  - $+ A $ Volts
* - $\texttt{0}$
  - $ -A$  Volts
```


```{figure} images/sec4-PAM-reception.png
:label: sec4-PAM-reception.png
:align: center 
Schéma de réception d’un signal PAM : filtrage pour réduire le bruit, échantillonnage aux instants TbTb​, et prise de décision par comparaison avec un seuil $\Gamma$ pour récupérer les symboles d’information.
```



Le récepteur PAM doit extraire l’information binaire du signal reçu.  Le signal reçu $r(t)$ est souvent bruité après la transmission. 
\begin{equation}
r(t) = s(t) + n(t)
\end{equation}
où \( n(t) \) est le bruit ajouté par le canal.
Un **filtre passe-bas** compatible avec la forme de l'impulsion  $p(t)$ (*matched filter*) est appliqué au  est utilisé pour atténuer le bruit et limiter l’interférence entre les impulsions/
Le signal filtré est échantillonné à des intervalles de temps $ T_b $, correspondant aux instants où chaque impulsion doit être détectée :
\begin{equation}
z_k = z(kT_b) = s_k + n_k
\end{equation}

Le récepteur applique une **règle de décision** pour déterminer si le symbole reçu correspond à un $\texttt{0}$ ou un $\texttt{1}$. Une **comparaison avec un seuil** $ \Gamma $ est effectuée :
\begin{equation}
\hat{b}_k =
\begin{cases}
    \texttt{1}, & \text{si } z_k \geq \Gamma \\
    \texttt{0}, & \text{si } z_k < \Gamma
\end{cases}
\end{equation}
où $\hat{b}_k $ est la décision du récepteur.
La synchronisation est nécessaire pour assurer l’alignement correct des échantillons avec les impulsions transmises.
 



:::{note}  Conception des impulsions $p(t)$ - Propriétés Désirées

La conception des signaux dans un système de communication repose sur plusieurs critères essentiels visant à optimiser les performances de transmission et de réception. L’un des objectifs fondamentaux est de minimiser la largeur de bande nécessaire pour transmettre l’information. En réduisant cette largeur de bande, on optimise l’utilisation du spectre et on diminue les interférences avec d’autres signaux. Le spectre de densité de puissance d’un signal reçu est donné par la relation suivante :
$$
S_y(f) = |P(f)|^2 S_x(f).
$$

Un autre critère important concerne la minimisation de la puissance requise. La puissance du signal doit être adaptée afin d’assurer un bon compromis entre la consommation énergétique et la performance du système. En particulier, la puissance transmise doit être suffisante pour garantir un faible taux d’erreurs tout en respectant les contraintes de bande passante.

La synchronisation est un élément clé dans la transmission des signaux. Il est essentiel que les formes d’ondes utilisées facilitent la récupération de l’horloge du signal reçu. Une bonne synchronisation permet d’éviter les décalages temporels pouvant entraîner des erreurs de détection et de décodage des symboles.

Un autre défi majeur dans la conception des signaux est d’éviter l’interférence entre symboles (*Inter-Symbol Interference*; ISI). Lorsque les symboles se chevauchent excessivement, la détection correcte des données devient difficile.
:::



#### Modulation numérique - $M$-aire - sans porteuse

Pour augmenter le débit de bits, nous pouvons envoyer plus de deux symboles.  Une approche consiste à l'utiliser $M$ symboles. 

```{figure} images/sec4-SymCod.png
:label: sec4-SymCod.png
:align: center 
Le schéma représente un codeur de symboles qui transforme une séquence $M$-aire en  symboles.
L'entrée du codeur est une séquence de bits $b_k$, $b(t)$ qui est ensuite transformée en un ensemble de signal de sortie $s(t)$, correspondant à des symboles spécifiques utilisés pour la transmission. Ce processus est essentiel dans les systèmes de communication numérique pour adapter les données binaires à un format compatible avec une modulation spécifique.
```

Le débit de bit entrant  et le débit de symboles sortant peuvent varier en fonction du nombre total de symboles uniques, $M$. Pour cette raison, deux indices temporels distincts sont utilisés :
- $k$ représente le **$k$-ième bit** dans la séquence binaire d’entrée ($a_k$).
- $n$ représente le **$n$-ième symbole** en sortie du codeur de symboles ($S_{1,n}$ et $S_{2,n}$).

Les principaux objectifs du codeur de symboles sont :
-  Regrouper les bits en symboles pour s’adapter aux techniques de modulation utilisées.
-  Améliorer l’efficacité spectrale, en adaptant le débit binaire au canal de transmission disponible.
-  Faciliter la démodulation et la récupération des données à la réception.

:::{tip} 
La période de bit correspond à la durée nécessaire pour transmettre un **bit unique** d'information. Elle est définie comme :
```{math}
T_b = \frac{1}{R_b}
```
où $R_b$ est le **débit de bits** (exprimé en bits par seconde, ou bps). La durée $T_b$ est directement liée à la fréquence de transmission des bits dans le système.
Un **symbole** peut représenter un ou plusieurs bits en fonction du schéma de codage utilisé. La période de symbole est la durée requise pour transmettre un **symbole complet**. Elle est définie comme :
```{math}
T_s = \frac{1}{R_s}
```
où $R_s$ est le **débit de symbole** (en symboles par seconde, ou baud). La relation entre $T_s$ et $T_b$ dépend du nombre de bits par symbole $M$ :
```{math}
T_s = \frac{T_b}{\log_2 M}
```
où $M$ est le nombre de symboles distincts utilisés à la sortie du codeur de symboles (utilisés dans la modulation).
- Si chaque symbole représente **un seul bit** ($M = 2$), alors $T_s = T_b$. La période de bit correspond à la durée nécessaire pour transmettre un **bit unique** d'information. Elle est définie comme :
- Si chaque symbole représente **plusieurs bits** ($M > 2$), alors $T_s > T_b$, ce qui permet de transmettre plus d'informations avec une fréquence de symboles plus faible.
:::




 
#### M-PAM « M-ary Pulse Amplitude Modulation » 

Le signal modulé en M-PAM (Modulation numérique  -  $M$-aire - sans porteuse) peut être exprimé mathématiquement par :
$$
\varphi_{M-PAM}(t) = \sum s_k p(t - kT_s)
$$
où $ s_k $ représente le symbole transmis appartenant à un ensemble de $ M$ symboles distincts ($ s_k \in \{s_1, s_2, \dots, s_M\} $), $ p(t)$ est la forme d’impulsion utilisée pour la transmission, et $ T_s$ est la période de symbole, définissant l’intervalle de temps entre chaque transmission de symbole. Cette modulation permet de transmettre une quantité d’information plus importante par unité de temps par rapport à une modulation binaire classique.

Dans un système M-PAM, chaque symbole peut encoder plusieurs bits, avec un nombre de bits par symbole défini par :
$$
L = \log_2(M)
$$

La détection d’un signal modulé en M-PAM  consiste à extraire les symboles transmis à partir du signal reçu. Ce processus implique plusieurs étapes essentielles permettant de minimiser les erreurs et d’optimiser la récupération de l’information.

Le signal reçu peut être modélisé comme  :
$$
r(t) = \varphi_{M-PAM}(t) + n(t) = \sum s_k p(t - kT_s) + n(t)
$$

où $ n(t) $ représente le bruit du canal.
La première étape de détection consiste à appliquer un filtrage adapté pour maximiser le SNR. Le filtre optimal $h(t)$ est choisi en fonction de $p(t) $, de manière à minimiser l’ISI.

Après le filtrage, le signal est échantillonné à des intervalles $ T_s $, produisant des valeurs discrètes :
$$
z_k = r(kT_s) = s_k + n_k
$$
où $n_k $ est le bruit affectant l’échantillon reçu.

 

Chaque échantillon $ z_k$ est comparé aux **niveaux de décision** correspondant aux $M $symboles possibles. Une **règle de décision** est appliquée en utilisant un détecteur à seuil  pour déterminer le symbole $\hat{s_k}$ reçu :
$$
\hat{s_k} = s_i, \quad \text{si } z_k \in \left[ \Gamma_{i-1}, \Gamma_i \right]
$$
où $ \Gamma_i $ sont les seuils de décision définis par :
$$
\Gamma_i = \frac{s_{i} + s_{i+1}}{2}, \quad i = 1, 2, ..., M-1
$$


 
Lorsque les signaux des messages sont aléatoires, nous devons utiliser leur spectre de densité de puissance, $S_m(f)$, pour déterminer sa largeur de bande. 
 

Le bruit introduit dans le canal peut entraîner des erreurs lorsque le signal reçu $ z_k $ est proche d’un seuil $ \Gamma_i $, conduisant à une **probabilité d’erreur de symbole** donnée par :
$
P_e = Q \left( \frac{d_{\text{min}}}{\sigma_n} \right)
$
où $ Q(\cdot) $ est la fonction de Q de Gauss, $d_{\text{min}} $ est la distance minimale entre deux niveaux de symboles, $ \sigma_n^2$est la variance du bruit.



:::{warning} Attention
Pour une puissance moyenne constante, plus le nombre de niveaux $ M $ augmente, plus les symboles sont rapprochés, ce qui augmente la sensibilité au bruit.  
:::
 
 
 ### Modulation numérique avec porteuse


 

#### ASK « Amplitude Shift Keying » 

ASK (modulation numérique  -  binaire - avec porteuse) est une technique  dans laquelle l’amplitude d’une onde porteuse varie en fonction des données binaires à transmettre avec un codeur de symboles :   
```{list-table}
:header-rows: 1
* - $b_k$ (Bit d'entrée [Binaire])
  - $s_k$ (Symbole de sortie [Tension])
* - $\texttt{1}$
  - $+ A $ Volts
* - $\texttt{0}$
  - $ 0$  Volts
```
Le signal modulé en **ASK** peut être exprimé comme suit :
$$
\varphi_{ASK}(t) = (s(t) * p(t) ) \times \cos(2\pi f_p t) = \sum_{k} s_k p(t - kT_b)\cos(2\pi f_p t) 
$$ 
 où $ \cos(2\pi f_p t) $ est la porteuse utilisée pour la modulation.

```{figure} images/sec4-ASK.png
:label: sec4-ASK.png
:align: center 
Dans la figure on peut observer ce processus en trois étapes distinctes. Une onde porteus est représentée comme un signal sinusoïdal continu, qui sera modulé en amplitude. Ensuite, la séquence binaire d’entrée est illustrée sous forme d’impulsions discrètes, correspondant aux bits transmis. Ces impulsions sont générées par le codeur de symboles, qui détermine comment chaque bit influencera le signal modulé. Enfin, la dernière partie de la figure montre le **signal modulé en ASK**, où la présence de la porteuse coïncide avec les bits **1**, tandis que son absence correspond aux bits **0**.
```
 

La démodulation du signal ASK  consiste à extraire le signal modulant binaire à partir du signal reçu. 
Le signal reçu peut être exprimé sous la forme :
\begin{equation}
r(t) = s(t) \cos(2\pi f_p t) + n(t)
\end{equation}

 
Pour récupérer l’information binaire, on multiplie le signal reçu avec la porteuse $ \cos(2\pi f_p t)$.   Un filtre passe-bas compatible avec la forme de l'impulsion  $p(t)$ (*matched filter*)  utilisé pour lisser le signal détecté et éliminer les hautes fréquences indésirables. Après filtrage, le signal obtenu est une version adoucie de l’enveloppe détectée.
Le signal filtré est échantillonné à des intervalles de temps $ T_b $ correspondant à la période des bits transmis,
\begin{equation}
z_k = z(kT_b) = s_k + n_k
\end{equation}. Chaque échantillon est comparé à un seuil $\Gamma$  pour décider de la valeur du bit reçu :
\begin{equation}
\hat{b}_k =
\begin{cases}
    \texttt{1}, & \text{si } r_k \geq \Gamma \\
   \texttt{0}, & \text{si } r_k  < \Gamma
\end{cases}
\end{equation}
Après la prise de décision, une séquence de bits est reconstruite. Ces bits correspondent aux données transmises avant la modulation ASK.

```{figure} images/sec-PSK-demod.png
:label: sec-PSK-demod.png
:align: center 
Schéma de démodulation cohérente d'un signal ASK, incluant la multiplication par la porteuse, le filtrage, l’échantillonnage et la prise de décision basée sur un seuil $\Gamma$.
```


Une **constellation** est utilisée pour la démodulation en associant chaque symbole reçu à l’un des points de la constellation. Après démodulation cohérente, le signal reçu $ r(t) $ est projeté sur la base d’onde $ \psi_1(t) $, donnant $z_k$ :
\begin{equation}
z_k = \int_{0}^{T_b} r(t) \psi_1(t) dt
\end{equation}
et $z_k$ est ensuite comparé aux seuils de décision $ \Gamma $ pour déterminer le symbole transmis $\hat{s}_k$. 
Ainsi, chaque point de la constellation permet une prise de décision robuste face au bruit, assurant une détection efficace du signal.


```{figure} images/sec4-ask-cons.png
:label: sec4-ask-cons.png
:align: center 
 Constellation du  ASK  avec seuil de décision $ \Gamma $. Les bits \texttt{1} et \textbf{0} sont représentés par $ A \cos(2\pi f_p t) $ et $ 0 $ respectivement.
```






####  PSK « Phase Shift Keying » 
PSK (modulation numérique  -  binaire - avec porteuse) est une technique  dans laquelle l’amplitude d’une onde porteuse varie sélon
```{list-table}
:header-rows: 1
* - $b_k$ (Bit d'entrée [Binaire])
  - $s_k$ (Symbole de sortie [Tension])
* - $\texttt{1}$
  - $+ A $ Volts
* - $\texttt{0}$
  - $ -A$  Volts
```
et le signal modulé est écrit par 
$$
\varphi_{PSK}(t) =  \sum_{k} s_k p(t - kT_b)\cos(2\pi f_p t) 
$$ 


```{figure} images/sec4-PSK-ex.png
:label: sec4-PSK-ex.png
:align: center 
Signal binaire (a) et signal modulé en phase (b) illustrant la modulation PSK.
```



La même règle de détection s'applique, mais le seuil doit être choisi en fonction du codeur de symboles. 
```{figure} images/sec4-bpsk-cons.png
:label: sec4-bpsk-cons.png
:align: center 
Constellation du BPSK avec seuil de décision $\Gamma$. Les bits $\texttt{1}$ et $\texttt{0}$ sont représentés par $ A \cos(2\pi f_p t) $ et $ -A \cos(2\pi f_p t) $ respectivement.
```
 



####  QPSK « Quandrature Phase Shift Keying »»


QPSK (Quadrature Phase Shift Keying) (modulation numérique  -  $M$-aire - avec porteuse) utilise deux porteuses en quadrature pour transmettre deux bits par symbole. Le signal modulé en QPSK est exprimé comme :

\begin{equation}
\varphi_{QPSK}(t) = s_1(t)\cos(2\pi f_p t) + s_2(t) \sin(2\pi f_p t)
\end{equation}
où $ s_1(t) $ et $ s_2(t) $ sont les sorties du codeur de symboles, représentant les deux bits modulés indépendamment sur les axes en phase (*In-phase*) et en quadrature (*Quadrature*).
Les deux signaux modulés sont additionnés pour former le signal $ \varphi_{QPSK}(t) $, qui peut transmettre deux bits par symbole, augmentant ainsi l’efficacité spectrale.

:::{warning} Attention
Notez qu'avec la présence d'une porteuse, deux flux de symboles indépendants peuvent être générés (pour le cosinus et le sinus).
```{figure} images/sec-SymEnc-2D.png
:label: sec-SymEnc-2D.png
:align: center 
Transformation d'une séquence binaire en une séquence de symboles bidimensionnels à l'aide d'un codeur. Chaque symbole est représenté par deux composantes indépendantes $s_1(t)$ et $s_2(t)$.
```
:::




Les avantages du QPSK son l'efficacité spectrale améliorée (doublement du débit binaire par rapport au BPSK) et robustesse au bruit (car les symboles sont espacés de $ 90^\circ $, réduisant les erreurs en présence d’interférences).


```{figure} images/sec4-qpsk-mod.png
:label: sec4-qpsk-mod.png
:align: center 
Schéma de modulation QPSK, combinant deux signaux modulants $ s_1(t) $ et $ s_2(t) $ sur des porteuses en quadrature $\cos(2\pi f_p t)$ et $\sin(2\pi f_p t)$.
```

```{figure} images/sec4-qpsk-ex.png
:label: sec4-qpsk-ex.png
:align: center 
La figure illustre le processus de génération d'un signal modulé en QPSK (2 bits par symboles).  La première courbe représente la séquence de bits d'entrée.
Le premier signal modulant $ s_1 $ (courbe verte) est issu des bits pairs. Le second signal modulant $ s_2 $ (courbe rouge) est issu des bits impairs.  $ s_1 $ module une porteuse en phase $ \cos(2\pi f_p t) $.
 $ s_2 $ module une porteuse en quadrature $ \sin(2\pi f_p t) $.  L'addition des deux donne le signal modulé en QPSK.
```

```{figure} images/sec4-qpsk-mod.png
:label: sec4-qpsk-mod.png
:align: center 
Schéma de modulation QPSK, combinant deux signaux modulants $ s_1(t) $ et $ s_2(t) $ sur des porteuses en quadrature $\cos(2\pi f_p t)$ et $\sin(2\pi f_p t)$.
```



Pour la demodulation,  le signal reçu  est multiplié par deux signaux de référence : 
     - Une porteuse en phase $ \cos(2\pi f_p t) $.
     - Une porteuse en quadrature $ \sin(2\pi f_p t) $, qui est obtenue en déphasant $ \cos(2\pi f_p t) $ de $ -\frac{\pi}{2} $.
 Après multiplication, chaque signal passe par un filtre passe-bas qui élimine les composantes haute fréquence et conserve uniquement les termes en bande de base.


 Les signaux en sortie des filtres correspondent aux coefficients $ z_{k,1} $ et $ z_{k,2}$, représentant les deux symboles.
Ses valeurs sont comparées à un seuil pour déterminer les bits correspondants.

 

```{figure} images/sec4-qpsk-cons.png
:label: sec4-qpsk-cons.png
:align: center 
Constellation du QPSK avec seuils de décision pour la détection des symboles.
```

## Resumé

Cette section traite de  **O4.**  *Proposition des techniques de modulation appropriées en fonction des caractéristiques du canal et du type d'information*, qui concerne   l'encodage et de la modulation des signaux numériques. Elle explore la conversion des séquences binaires en séquences de symboles à l'aide de codeurs, la modulation d'amplitude et de phase (PAM, PSK, QPSK), ainsi que leur démodulation et détection via des constellations. L'impact du débit binaire et du débit symbolique sur les performances du système est également abordé.


%- **QAM « Frequency Shift Keying »»**


%Modulation numérique  -  $M$-aire - avec porteuse


% - **Modulation**  
%- **Efficacité énergétique** 

%- **Efficacité spectrale**

%- **Démodulation cohérente (synchrone)**



% - **Modulation**  
%- **Efficacité énergétique** 

%- **Efficacité spectrale**

%- **Démodulation cohérente (synchrone)**


 %Modulation par onde porteuse
%4.1. Modulation d'amplitude
%4.2. Modulation d’angle
%4.3. Modulation numérique


 


%#### Largeur de Bande de Transmission - PCM Binaire

%Pour un **PCM binaire**, chaque échantillon est quantifié en utilisant $L$ niveaux de quantification, chaque échantillon est codé sur $N$ bits.  Si le signal analogique $ m(t)$ est **limité en fréquence** à $ B $ Hz, **le théorème de Nyquist** impose un minimum de $ 2B $ échantillons/sec pour une reconstruction parfaite.  Comme chaque échantillon est représenté par $ N $bits, le **débit binaire total** est :
%  $$
%  R_b = 2NB \quad \text{bits/sec}
%  $$
%et donc la **largeur de bande minimale** nécessaire pour la transmission de la sortie de PCM est :
 % $$
 % B_{T,\min} = \frac{R_b}{\eta_{\text{spectrale-binaire, max}}} = NB \quad \text{Hz}
 % $$
%[Lahti&Ding 5e édition:  Équation 5.37, page 312]. 


%Yapilacaklar - LSB-SSB sekil koy (yeni ciz)
%Spectral efficiecny discussioni ekle  (SSB oncesinde)




%L’information est contenue uniquement dans les **bandes latérales** (*side-bands*), nécessitant une démodulation synchrone pour la récupération du signal.

%La modulation **DSB-SC** est donc plus efficace en **énergie** que la modulation AM standard, mais elle n’optimise pas l’usage du **spectre**, contrairement à la modulation à bande latérale unique (SSB).




