# SWAN Universal Basic Income (UBI)

1. **Purpose**: The UBI system in SWAN is designed to ensure that providers in the network are compensated for their participation, even if they aren't actively engaged in jobs. This ensures a stable and active network of providers, ready to take on tasks as they come.
2. **Provider's Income**:
   * Every provider has the potential to earn from two sources: the jobs they complete and the UBI.
   * If a provider's income from jobs (denoted as ( J )) is less than or equal to the UBI amount (denoted as ( U )), they receive the UBI as their total income.
   * If a provider's job income exceeds the UBI, they rely solely on their job income.
3. **UBI Rate Adjustment**:
   * The UBI rate is dynamically adjusted based on the network's activity. If the current UBI rate (denoted as ( R )) exceeds a target rate (denoted as ( k )), system jobs (Network Tasks) are introduced to balance the rate.
   * The number of system jobs introduced is proportional to the difference between the current and target UBI rates.
4. **Budget Allocation**:
   * The total budget for the UBI system comes from the SWAN Treasure DAO. This budget is allocated among UBI, Network Tasks, and Creator Rewards.
   * Specific percentages of the total budget are allocated to each of these categories.
5. **Eligibility for UBI**:
   * Not all providers automatically qualify for UBI. They must achieve a certain reputation score to be eligible.
   * Providers with a reputation score below a threshold are not eligible for UBI.
6. **Compensation Mechanism**:
   * If a provider's job income is less than the UBI, they receive compensation to bridge the gap. This ensures that providers are incentivized to take on more jobs rather than relying solely on UBI.
7. **Proof of Eligibility**:
   * To prevent misuse, providers must periodically submit proofs (e.g., zk proofs) to demonstrate that they own the hardware they claim. This ensures that only genuine providers benefit from the UBI.
8. **System Jobs and Creator Rewards**:
   * When the UBI rate exceeds the target, the system introduces Network Tasks to provide more job opportunities.
   * Additionally, to encourage more job creation, creators are rewarded for placing jobs in the system.
9. **Governance**:
   * The SWAN Treasure DAO manages the UBI system's budget. Decisions regarding budget allocation, UBI rate adjustments, and other critical parameters are made by a committee. This committee comprises token holders, core developers, and other contributors.

In essence, the SWAN UBI system is a dynamic and adaptive mechanism designed to maintain a healthy, active, and incentivized network of providers. It balances the needs of providers with the overall health and activity of the network.

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

&#x20;Where  $$\alpha, \beta, \gamma \$$$$\alpha, \beta, \gamma$$ are the respective allocation percentages for UBI, Network Tasks, and Creator Rewards, and $$\alpha + \beta + \gamma = 1$$.

**Eligibility for UBI**:

* Let ( r ) be the reputation score of a provider and ( T ) be the threshold score (e.g., 60).&#x20;

$$\text{Eligibility} =       \begin{cases}       \text{True} & \text{if } r \geq T \\      \text{False} & \text{otherwise}      \end{cases}$$

**Compensation Mechanism**:

For a provider's job income ( J ) and UBI ( U ):&#x20;

$$\text{Compensation} =       \begin{cases}       U - J & \text{if } J \leq U \\      0 & \text{if } J > U       \end{cases}$$

