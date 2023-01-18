# FEATURES

Swan Provider listens to offline deals that come from the Swan platform. It provides the following functions:

* Download offline deals automatically using aria2 for downloading service.
* Publish `PublishStorageDeals`messages, moves funds from collateral wallet into escrow with the StorageMarketActor(when set `Market_version=1.2`)
* Import deals using Market(version=1.1 and 1.2) once the download is completed.
* Synchronize deal status to [Swan Platform](https://console.filswan.com/#/dashboard), so that both clients and storage providers will know the status changes in real time.
* Auto-bid task from FilSwan bidding market.
* Get the manual-bid tasks from the FilSwan Platform.
