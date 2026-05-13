# Definition
Om  $$\Large x_1, x_2, \dots, x_n$$
är ett stickprov på $\Large X$ med $\Large\theta$ i sin sannolikhetsfördelning så ör **Likelihoodfunktionen för parametern $\Large \theta$:
$$\Large
\mathcal{L}(\theta) = 
\begin{cases}
\prod_{i=1}^n p(x_i; \theta) \quad \text{om } X \text{  är diskret}\\
\prod_{i=1}^n f(x_i; \theta) \quad \text{om } X \text{  är kontinuerlig}\\
\end{cases}
$$
---
# Maximum Likelihood Estimation (MLE)
Givet
$$\Large
\mathcal{L}(θ) = \prod_i f(x_i; θ)$$
Är skattningen på $\theta$ 
$$\Large
θ_{MLE} = \arg\max_\limits{\theta \in [0, 1]}  \mathcal{L}(θ) $$
---
# Steg för att hitta MLE
1. Ta produkten av alla täthetsfunktioner: $$\Large \mathcal{L}(\theta) = \prod f(x)$$ 
2. Hitta sedan log-likehood funktionen av produkten: $$\Large \ell(\theta) =ln(\mathcal{L}(\theta) )$$ 
3. Ta sedan derivatan av log produkten lika med noll. $$\Large \frac{\partial}{\partial \theta} (\ell (\theta)) = 0$$
4. Lös ut $$\Large \theta_{MLE}^*$$
---
# Problem med MLE
Vid t.ex. ett mynt kast finns det en 50% chans för bägge utfall, men ifall våran distribution enbart har medvetenhet av en liten mängd kast eller enbart ena sidan kan vi få en 

$$\Large
\theta_{\text{MLE}} = 0
$$
Vilket innebär att MLE inte har någon medvetenhet av våra föregående tro eller distribution

---
# Links
[[Matematisk Statistik]]
[[Machine Learning]]
