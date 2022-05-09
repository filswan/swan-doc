# Basic Concepts

Swan Provider provides the following functions:

* Download offline deals automatically using aria2 for downloading service.
* Import deals using lotus once the download is completed.
* Synchronize deal status to [Swan Platform](https://www.filswan.com), so that both clients and miners will know the status changes in real-time.
* Auto bid task from FilSwan bidding market.
* Delete CAR files under the downloaded directory in the status "Completed, DealExpired, or ImportFailed"
* Set CAR files' status "StorageDealError" to "ImportFailed" directly without downloading them.
