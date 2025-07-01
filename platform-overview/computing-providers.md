# Computing Providers

A Computing Provider (CP) is a third-party individual or organization that offers scalable computing resources, which businesses can access on demand over Swan network. These resources include cloud-based compute, storage, platform, and application services.

As a resource provider, you can run a **ECP** (Edge Computing Provider) and **FCP** (Fog Computing Provider) to contribute yourcomputing resource.

* **ECP (Edge Computing Provider)** specializes in processing data at the source of data generation, using minimal latency setups ideal for real-time applications. This provider handles specific, localized tasks directly on devices at the network’s edge, such as IoT devices. At the current stage, ECP supports the generation of **ZK-Snark proof of Filecoin network**, and more ZK proof types will be gradually supported, such as Aleo, Scroll, starkNet, etc. Check  [Install Guideline](https://docs.swanchain.io/bulders/computing-provider/edge-computing-provider-ecp/ecp-setup) here.
* **FCP (Fog Computing Provider)** Offers a layered network that extends cloud capabilities to the edge of the network, providing services such as AI model training and deployment. This provider utilizes infrastructure like Kubernetes (K8S) to support scalable, distributed computing tasks. **FCP** will execute tasks assigned by Market Provider, like [Orchestrator](https://orchestrator.swanchain.io/) on the [Swan chain](https://swanchain.io/). Check [Install Guideline](https://docs.swanchain.io/bulders/computing-provider/fog-computing-provider-fcp/computing-provider-setup) here.

For the current status of Swan Provider Network, please check here: [https://provider.swanchain.io](https://provider.swanchain.io/overview)

### **Address Types**

A CP account has three different wallet addresses to ensure security and separation of responsibilities:

* `ownerAddress`: This is the owner account of the CP account. The owner has permission to change account information such as the multi-address, worker address, and beneficiary address. In most situations, the private key of the `ownerAddress` does not need to be present on the server for security reasons.
* `workerAddress`: This is the actual working address used for submitting proofs (`submitProof`). It needs to be funded with a certain amount of ETH to pay for gas fees when submitting proofs.
* `beneficiaryAddress`: This is the address where all earnings from the CP account will be sent. It is solely used for receiving funds. For security purposes, the private key of the `beneficiaryAddress` should not be stored on the server to maintain isolation.

By separating these address, the system ensures that only the necessary `workerAddress` private key is present on the server, while the more sensitive `ownerAddress` and `beneficiaryAddress` private keys are kept separate, enhancing the overall security of the system.

[**More Details**](https://docs.swanchain.io/bulders/computing-provider)
