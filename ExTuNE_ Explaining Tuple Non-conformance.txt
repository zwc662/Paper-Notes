


# [ExTuNE: Explaining Tuple Non-conformance](http://dbgroup.cs.umass.edu/?p=860)

* **Data invariant** is featured by a set of constraints on the tuples in the dataset.
* **Non-conformance** means that a test tuple violates the data invariant constraints 
*  Data invariant may not provide interpretable explanations of non-conformance.
* **Non-conforming tuples** are tuples on which a machine-learned model makes untrustworthy predictions. Those tuples ... 	   	
	 * introduces uncertainty
	 * are not exactly equivalent to outliers as some outliers may not be non-forming 
> `Example 1.1` Consider a dataset $\{(1, 10), (2, 20), (4, 40)\}$ and two new tuples $t_1=(3, 12), t_2 =(10, 100)$. A traditional distance-based outlier detector will mark $t_2$ as outlier as its distance is further away from the dataset than that of $t_1$. However, obviously $t_2$ is more likely to be conforming in the sense of $t[1]=10t[0]$. From this perspective, $t_1$ is the non-forming one.

## Contributions
1. No prior work explains outliers based on which attributes or attribute relationships are responsible for non--conformance.
2. EXTUNE predicts non-conforming data as if they belong to a negative class. But unlike binary classifiers, EXTUNE do not have prior knowledge of two-class labels and the data are not labelled at all in the beginning.

## Solution

### Find Data Invariants
* An invariant learner learns data invariants from the training tuples. When a new tuple arrives, EXTUNE checks if the test tuple satisfies the invariant, and if it does not, EXTUNE quantifies the degree of non-conformance.
* `Inverted PCA` low-variance principal components are the most useful predictors of non-conformance. Use low-variance principal components to predict non-conformance
* For a dataset $D$, the data invariant $I$ is in the form of "the projection of each tuple in $D$ onto the low-variance component results in values that lie within XXX standard deviations from the mean of the corresponding projection"
* Data invariant is a constraint that defines a set of conforming tuples and $x\vdash I$ denotes that the tuple $x$ belongs to the conforming tuple set.
* Use violation function $violation(x, I)$ to quantify the degree of invariant violation by a tuple. It is the distance of the tuple $x$ from the invariant $I$.
$$violation(x, I)= 
\begin{cases}
    0& x\vdash I\\
    1,              & x\nvdash I
\end{cases}
$$
* A weighted sum over violation values evaluates the aggregated violations. The low-variance invariants are more weighted, and the high-variance less weighted.

### Causality of Non-Conformance
* Measure the responsibility of attributes for causing non-conformance
* **Counterfactual cause** 
	* Altering values of an attribute to the mean, and observe how it affects the invariant violation.
	* For tuple $x=(x_0, x_1, \ldots, x_m)\nvdash I$, $x_i$ is the cause for the violation if $x=(x_0, x_1, \ldots, \mu_i, \ldots, x_m)\vdash I$ where $\mu_i$ is the mean of $i$th attribute in the dataset.
* **Actual cause**
	* An attribute is the actual cause of violation if it is a counterfactual cause of the violation only if other non-counterfactual cause attribute values are allowed to be altered into the mean. The alterations are called *contingencies*
	* **Minimal support** is the minimum number of altered attribute value alterations required for an attribute to become a counterfactual cause.
	* Responsibility of an attribute is $\frac{1}{M+1}$ if it becomes a counterfactual cause with at least $M$ contingencies.
* **Approximating Minimal Contingency**
	* Finding the minimal contingency for an actual cause is an NP-hard problem. A greedy approach is used to find an approximation. It does not guarantee optimality.
	* Iteratively selects attributes to alter based on their contribution to the invariant violation. The attribute with the highest weighted violation value is altered first.
* The responsibility of a tuple for each invariant are aggregated in that the responsibility values are weighted by the violation values and added.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTExMzg3MTMxMjJdfQ==
-->