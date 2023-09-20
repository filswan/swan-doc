# SWAN Universal Basic Income (UBI)

**Objective:** The primary goal of SWAN's UBI is to provide a safety net for providers, ensuring they receive a minimum income regardless of the jobs they secure. This mechanism ensures stability in the network, incentivizing providers to remain active and maintain their infrastructure, even during periods of low job availability.

**Eligibility Criteria:**

1. **Proof of Eligibility:** Providers must prove they own the hardware they claim. This is done through regular submissions, such as zk-proofs, to validate their claims.
2. **Reputation Score:** A provider must achieve a minimum reputation score (e.g., 60) to be eligible for UBI. This score ensures that only genuine and active providers benefit from the UBI.
3. **Job Threshold:** If a provider doesn't secure a job within a specified block time (e.g., 6000 blocks), they risk being blacklisted. However, during this period, they are eligible for UBI.

**Compensation Mechanism:**

1. If a provider's job income (J) is less than or equal to the UBI (U), they receive the UBI amount. Essentially, if $$J<U$$, the total income is $$U$$.
2. If a provider's job income surpasses the UBI, they only receive their job income and no UBI.

**Dynamic Adjustments:** The UBI rate is dynamically adjusted based on the network's overall job rate. If the current UBI rate exceeds a target rate (e.g., 7%), the system triggers the creation of system jobs (Network Tasks) to incentivize providers to take on more jobs. This mechanism ensures that the UBI doesn't become a crutch but rather a safety net, pushing providers to actively seek jobs.

**Budget Allocation:** The UBI is funded from the SWAN Treasure DAO, which manages the budget for UBI, Network Tasks, and Creator Rewards. The allocation for UBI is determined based on the total budget and the current needs of the network.

**Benefits:**

1. **Stability:** Ensures a stable and active provider base, even during low job demand periods.
2. **Inclusivity:** Allows smaller providers to compete and remain active in the network.
3. **Network Health:** By ensuring providers are compensated, the network maintains a healthy number of active nodes, ensuring redundancy and robustness.

In summary, the SWAN UBI is a strategic tool to maintain an active and healthy network of providers, ensuring that they are compensated fairly and incentivized to actively seek and complete jobs.
