# Swan Provider Income

### **1. Introduction**

In the Swan decentralized computing ecosystem, providers earn income by executing jobs. Their income is influenced by various factors, including the number of jobs they execute, their reputation, and the Universal Basic Income (UBI) mechanism. This document outlines the mathematical model governing provider income in the Swan system.

### **2. Job Allocation to Nodes**

Job distribution in the Swan system is done through an auction mechanism. However, the likelihood of a provider winning a job is influenced by their reputation. The job distribution engine follows a lambda distribution based on reputation scores.



$$
P_{win}(R) = \lambda \times e^{-\lambda R}
$$

Where:

* ( P\_{win}(R) ) = Probability of winning a job based on reputation ( R )
* ( \lambda ) = Rate parameter (determined by the system)

### **3. Total Jobs in the System**

The total number of jobs in the system grows according to the logistic growth curve:

$$
J_{total}(x) = \frac{L_{initial}}{1 + e^{-k_{initial} \times (x - x_{0_{initial}})}}
$$

Where:

* ( J\_{total}(x) ) = Total number of jobs at time ( x )
* ( L\_{initial} ) = Carrying capacity for initial jobs (maximum number of jobs without incentives)
* ( k\_{initial} ) = Growth rate for initial jobs
* ( x\_{0\_{initial\}} ) = Midpoint of the growth curve, where growth is fastest

### **4. Base Income from Jobs**

Providers earn a base income from executing jobs. This income is determined by the auction mechanism, where providers bid for jobs.



$$
I_{base}(j) = P_j \times N_j
$$

Where:

* ( I\_{base}(j) ) = Income from job ( j )
* ( P\_j ) = Price bid for job ( j )
* ( N\_j ) = Number of instances of job ( j ) executed

### **5. Universal Basic Income (UBI)**

Qualified providers receive a UBI. However, if a node has job income, the UBI is reduced by that amount. If the job income exceeds the average UBI, the UBI becomes zero.

\[ I\_{UBI} = U - min(I\_{total\_jobs}, U) ]

Where:

* ( I\_{UBI} ) = UBI income
* ( U ) = Average UBI income
* ( I\_{total\_jobs} ) = Total income from all jobs

### **6. Bonus from Reputation**

Providers with higher reputations can earn more due to a higher likelihood of winning bids in the auction system.



$$
I_{bonus}(R) = \lambda \times e^{-\lambda R}
$$

Where:

* ( I\_{bonus}(R) ) = Bonus income based on reputation ( R )

### **7. Total Provider Income**

The total income for a provider is the sum of the base income from jobs, the UBI, and any bonuses from reputation.



$$
I_{total} = I_{base} + I_{UBI} + I_{bonus}
$$

#### **8. Conclusion**

The Swan provider income model ensures a balanced distribution of income, rewarding providers for their service quality (reputation) and ensuring a safety net through the UBI. This comprehensive approach ensures the sustainability and attractiveness of the Swan ecosystem for potential providers.
