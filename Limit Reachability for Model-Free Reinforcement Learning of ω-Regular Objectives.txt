# [Limit Reachability for Model-Free Reinforcement Learning of -Regular Objectives](https://dl.acm.org/doi/abs/10.1145/3313149.3313369?casa_token=FIG7h10Z8wsAAAAA:Y11idRzHhusvSYEKhtnpQ32EvL8nQd2_urnzvAwX6ZNY53TZYuAvVxZ7WcXmRKG98lr3v-dyII-QvA)

* Accidents involving learning-enabled systems have received intense publicity and concern.
* Logic provides a foundation for the rigorous specification of learning objectives.
* Model-free reinforcement learning supported by neural networks promises scalability.
* It is important to be able to translate logic-based requirements-specifically, $\omega$-regular objectives-into the scalar rewards, called $\omega$-regular reward. The problem has been solved.
* A key problem for the proposed translation approach is that if the same reward is meted out whenever an accepting transition is crossed, then the frequency at which rewards are obtained affects the desirability of a strategy
* __Limit Reachability (LR)__ reduces the _search for a policy that maximizes the probability of satisfying an $\omega$-regular objective_ to the _search for a policy that maximizes a reachability probability_
* The composition of an MDP and a _limit-deterministic Buchi automaton (LDBW)_ is connected to an auxiliary target state by transitions whose probability is controlled by a parameter $\xi$. 
	* When $\xi\rightarrow 1$, the exact satisfaction probability is obtained. 
	* Granting positive rewards probabilistically whenever the LDBW driven by the observations of the MDP takes an accepting transition
	*	The probability of reaching a winning end component in the MDP is upper bounded by the probability of reaching the target from the initial state of the product of MDP and LDBW.
	> Let $p_s(\xi)$ be the probability of reaching state $t$ from state $s$ in the augmented product MDP. Then the probability of satisfying the $\omega$-regular objective from $s$ is $\bar{lim}_{\xi\rightarrow 1}. p_s(\xi)$.
* Usually **Deterministic Rabin Automaton (DRW)** is used in the analysis of MDPs instead of **Deterministic Buchi Automaton (DBW)**, because the latter cannot express all $\omega$-regular objectives. 
*  Meanwhile, **Nondeterministic Buchi Automaton (NBW)** is not used because causal strategies cannot optimally resolve nondeterministic choices due to its requirements on accessibility to future events
* A LDBW is an NBW that behaves deterministically once it has seen an accepting transition. LDBW is as expressive as general NBWs, while NBWs can be translated into suitable LDBWs for qualitative and quantitative analysis of MDPs
* The product of MDP and LDBW is not build but the observations of the MDP are used by an interpreter process to compute a run of the objective automaton. When a transition is accepted, the interpreter gives the learner a positive reward with probability $1-xi$. When the agent receives a reward, the training episode terminates. Any RL that maximizes this probabilistic reward is guaranteed to converge to an optimal policy
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNjM3NjY1MThdfQ==
-->