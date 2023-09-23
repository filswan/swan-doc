# Universal Basic Income (UBI)

#### **1. Introduction**

In the Swan decentralized computing ecosystem, the Universal Basic Income (UBI) model aims to provide a basic level of compensation to qualified providers. This document outlines the specific requirements and mechanisms for the implementation of UBI within Swan.

#### **2. UBI Eligibility**

**2.1 Hardware Performance**

* Providers must meet a minimum hardware performance threshold to qualify for UBI.
* The performance can be benchmarked using algorithms like zk-proof, ensuring that the provider's hardware is capable of supporting the ecosystem's computational needs.

**2.2 Proof of Ownership**

* Providers must demonstrate proof of ownership of their hardware resources.
* This proof should be posted on-chain, ensuring transparency and verifiability.

#### **3. UBI Calculation**

**3.1 Base UBI**

Every qualified provider in the Swan ecosystem is eligible to receive a base UBI amount.

**Equation**:&#x20;

$$
UBI_{base} = V_{ubi}
$$



Where:

* ( UBI\_{base} ) is the base UBI for the provider.
* ( V\_{ubi} ) is the value of the UBI in Swan Tokens.

**3.2 Job Income Deduction**

If a provider earns income from jobs, this income will be deducted from their UBI. If their job income exceeds the average UBI, they will not receive any UBI.

**Equation**:



$$
UBI_{net} = UBI_{base} - I_{job}
$$

Where:

* ( UBI\_{net} ) is the net UBI after deducting job income.
* ( I\_{job} ) is the income earned from jobs.

**Condition**:&#x20;



$$
if ( I_{job} ) >= ( UBI_{avg} ), then ( UBI_{net} ) = 0
$$

Where:

* ( UBI\_{avg} ) is the average UBI income.

#### **4. Funding UBI**

The funds for UBI can be sourced from:

* A portion of the fees collected from job creators.
* A reserve fund set up by Swan during its initial token offering or fundraising.
* Voluntary contributions from larger providers or stakeholders.

#### **5. Periodic Review**

The UBI model, eligibility criteria, and funding sources should be reviewed periodically. This ensures that the system remains fair, sustainable, and aligned with the evolving needs of the Swan ecosystem.

#### **6. Conclusion**

The UBI model in the Swan ecosystem ensures that qualified providers receive a basic income, promoting inclusivity and fairness. By setting clear eligibility criteria and adjusting UBI based on job income, Swan ensures a balanced distribution of resources and rewards within its decentralized computing platform.
