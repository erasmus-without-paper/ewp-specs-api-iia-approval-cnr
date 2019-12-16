Interinstitutional Agreement Approval CNR API
=============================================

* [What is the status of this document?][statuses]
* [See the index of all other EWP Specifications][develhub]


Summary
-------

This document describes the **Interinstitutional Agreement Approval CNR API**.
This API can be implemented by all EWP partners, and will be called by some
other EWP partners whenever related IIAs are approved by them. It allows
the partners to listen for approvals of their copies of the IIAs.

CNR stands for Change Notification Receiver. For a detailed introduction on how
CNR APIs work, please read [this page][cnr-intro].


Request method
--------------

 * Requests MUST be made with HTTP POST method. Servers MAY reject all other
   request methods.


Request parameters
------------------

Parameters MUST be provided in the regular `application/x-www-form-urlencoded`
format.


### `approving_hei_id` (required)

Identifier of the HEI which has recently approved the partner's copy of the IIA
and is now sending the notification about this event.

Server implementers SHOULD verify if the request is signed with a proper client
certificate bound to this HEI.


### `owner_hei_id` (required)

Identifier of the HEI which is the owner of the copy of the agreement, that has been approved.
Together with `iia_id`, uniquely identifies the agreement copy.


### `iia_id` (required)

Partner's identifier of the IIA which has been approved. **Note: ** this is NOT the ID assigned
by the notifier (approving HEI), but by the owner of the copy which has been approved.


Security
--------

This version of this API uses [standard EWP Authentication and Security, Version 2][sec-v2].
Server implementers choose which security methods they support by declaring them
in their Manifest API entry.


Handling of invalid parameters
------------------------------

 * General [error handling rules][error-handling] apply.

 * Servers MUST return a valid (HTTP 200) XML response whenever the request has
   been [properly received][bad-cnr-request]. Unless HTTP 200 is received,
   clients are RECOMMENDED to automatically retry the request after some time.


Response
--------

Servers MUST respond with a valid XML document described by the
[response.xsd](response.xsd) schema. See the schema annotations for further
information.


Keep in mind that...
--------------------

It is NOT guaranteed that all notifications will be delivered to you promptly.
Some notifications may also **not reach you at all**. Also, not every server
sends such notifications (look for `<sends-notifications/>` element in
[IIAs Approval API][iias-approval-api]'s manifest entries to get a clue which servers do).


[bad-cnr-request]: https://github.com/erasmus-without-paper/ewp-specs-architecture#bad-cnr-request
[cnr-intro]: https://github.com/erasmus-without-paper/ewp-specs-architecture#cnr
[develhub]: http://developers.erasmuswithoutpaper.eu/
[error-handling]: https://github.com/erasmus-without-paper/ewp-specs-architecture#error-handling
[iias-approval-api]: https://github.com/erasmus-without-paper/ewp-specs-api-iias-approval
[sec-v2]: https://github.com/erasmus-without-paper/ewp-specs-sec-intro/tree/stable-v2
[statuses]: https://github.com/erasmus-without-paper/ewp-specs-management#statuses
