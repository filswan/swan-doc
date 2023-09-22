# Universal Basic Income (UBI)

**Purpose:** The Universal Basic Income (UBI) system in SWAN is designed to ensure that computing providers within the network are fairly compensated for their participation, even if they aren't actively engaged in tasks or jobs. This promotes a stable and active network of providers, always ready to undertake tasks as they arise.

**Provider's Income:** Every provider in the SWAN network has two potential sources of income:

1. **Jobs:** Payments received for the tasks or jobs they complete.
2. **UBI:** A fixed income provided to eligible providers, irrespective of the jobs they undertake.

If a provider's income from jobs is less than the set UBI amount, they will receive the UBI as their total income. However, if their job income exceeds the UBI, they will rely solely on their job income.

**Public Service Jobs:** These are tasks created by the SWAN Treasure for public service purposes. The jobs can stem from various sources, including scientific research, demonstrations of use cases, or storage/computing needs within the SWAN ecosystem. Not only do these jobs provide valuable services to the public and the SWAN ecosystem, but they also serve as a mechanism to ensure providers have consistent work. When there's a shortage of external jobs in the system, Public Service Jobs help fill the gap and ensure providers remain active and compensated.

**UBI Rate Adjustment:** The UBI rate is dynamically adjusted based on the overall activity within the network. If the current UBI rate exceeds a predetermined target rate, more Public Service Jobs are introduced to provide additional work opportunities and balance the rate. This approach ensures that providers remain engaged and the UBI rate is kept in check.

**Budget Allocation:** The entire budget for the UBI system is sourced from the SWAN Treasure DAO. This budget is then distributed among different categories, namely UBI, Network Tasks, and Creator Rewards. Specific percentages of the total budget are allocated to each of these categories.

**Eligibility for UBI:** Not every provider in the network is automatically entitled to UBI. To qualify, providers must achieve a certain reputation score. Those with a reputation score below a set threshold are deemed ineligible for UBI.

**Proof of Eligibility:** To prevent any misuse or fraudulent activities, providers are required to periodically submit proofs, such as zk proofs, to validate that they genuinely own the hardware they claim to. This ensures that only legitimate providers benefit from the UBI.

**Governance:** The governance of the UBI system is overseen by the SWAN Treasure DAO. This body is responsible for making critical decisions related to budget allocation, UBI rate adjustments, and other essential parameters. The decision-making committee comprises token holders, core developers, and other significant contributors.

### Structured Representation

**Provider's Income**:

For a provider's job income ( **J** ) and UBI ( **U** ):&#x20;

$$\text{Total Income} =       \begin{cases}       U & \text{if } J \leq U \\      J & \text{if } J > U       \end{cases}$$

**UBI Rate Adjustment**:

Let   **R**  be the current UBI rate and   k  be the target UBI rate.

$$
S = 
     \begin{cases} 
     n \times (R - k) & \text{if } R > k \\
     0 & \text{otherwise}
     \end{cases}
$$

&#x20; Where  S  is the number of system jobs (Network Tasks) and ( n ) is a constant multiplier.

**Budget Allocation**:

Let ( B ) be the total budget from the SWAN Treasure DAO.&#x20;

$$
A_U = \alpha \times B, \quad A_N = \beta \times B, \quad A_C = \gamma \times B
$$

&#x20;Where  $$\alpha, \beta, \gamma \$$$$\alpha, \beta, \gamma$$ are the respective allocation percentages for UBI,Public Service Jobs, and Creator Grants, and $$\alpha + \beta + \gamma = 1$$.

**Eligibility for UBI**:

* Let ( r ) be the reputation score of a provider and ( T ) be the threshold score (e.g., 60).&#x20;

$$\text{Eligibility} =       \begin{cases}       \text{True} & \text{if } r \geq T \\      \text{False} & \text{otherwise}      \end{cases}$$

**Compensation Mechanism**:

For a provider's job income ( J ) and UBI ( U ):&#x20;

$$\text{Compensation} =       \begin{cases}       U - J & \text{if } J \leq U \\      0 & \text{if } J > U       \end{cases}$$

