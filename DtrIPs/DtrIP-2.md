---
DTrIP: 2
title: Booking Referral Rewards
description: Allows referrers to receive part of a booking's fees for referring a booking.
author: Perito Moreno (@PeritoM)
discussions-to: https://dtravelworkspace.slack.com/archives/C02H2KZDW2C/p1660222547003739
status: Draft
category: Booking Contract Improvement, BackEnd Improvement, FrontEnd Improvement
---


## Abstract

The current booking contract splits payments between the host and the Dtravel treasury. This DTrIP proposes to:
- modify the payment contract so that a fraction of the fee that would be going to Dtravel treasury goes to the referrer instead.
- Modify the back-end and the front-end accordingly, so that the referrer is included in the booking details given to the contract.


## Motivation

In order to drive more bookings, we would like to incentivize others (Dtravel ambassadors, our partner PMSs, organizers of crypto conferences with whom we partner, builders of curated lists of Dtravel listings…) to refer Dtravel to potential guests.


## Specification

_The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119._

- [X] The smart contract's booking struct should be extended with the address of the referrer. 
- [X] The config smart contract should have an additional updatable variable storing the percentage referral fee.
    - [X] It should not be possible to set the percentage referral fee higher than the overall percentage fee.
- [X] The smart contract's payout and cancel functions should be modified in such a way that the referral fee is sent to the referrer's address and the total fee minus the referral fee should be sent to the Dtravel treasury.
- [ ] The booking website for a Dtravel listing should take the referrer's address as a URL parameter.
- [ ] The Dtravel backend should maintain a whitelist of authorized referrer addresses.
    - [ ] There should be a frontend for Dtravel to add new addresses of referrers to the whitelist.
- [ ] Before calling the booking smart contract to make a booking with a referrer, Dtravel's backend must check that the referrer's address is in the whitelist.
- [ ] Smart contract modifications should be tested.
- [ ] Backend and frontend modifications should be tested.


## Rationale

Besides a booking referral reward program, we have also considered a host onboarding referral reward program. The latter is also possible, but it is more complex. Moreover, a booking referral reward program may be sufficient to encourage referrers to refer new hosts for onboarding as well, since more onboarded hosts mean more opportunity for earning booking referral rewards later. Both types of referral rewards could co-exist in the future. This DTrIP focuses on booking referral rewards, but we could have another DTrIP for host onboarding referral rewards in the future.

Instead of receiving the referrer's address as a URL parameter, the booking website of a Dtravel listing could allow the guest to include the address of the referrer in an input text box. We suggest leaving this option out-of-scope for now because it requires more work and also because it would require incentivizing the guest to perform this manual step by, for instance, giving part of the referral rewards to the guest as well. Furthermore, as a guest who doesn't have a referral code to include, it can be a disappointing experience to see an input box asking for a referral code.

Instead of using a wallet addresses as a referral code, we could use generated referral codes and maintain a map between generated codes and addresses in the backend. We left this option out-of-scope for now, because it is not strictly necessary. But it is something that could be done in the future.

The whitelist could be implemented in the smart contract instead of the backend. This DTrIP proposes the latter, because it is simpler and because, anyway, our smart contract's `book` function can only be called with data signed by our backend at the moment. However, once DTrIP #1 gets implemented and our backend is not the only data provider anymore, we will need to implement the whitelist in the contract instead. 

We could also have a booking referral reward system by the hosts, where the hosts can authorize referrers and have referral rewards deducted from their own revenue, instead of from Dtravel's treasury fee.



## Backwards Compatibility

This proposal is not backwards compatible. For referral rewards to be received for bookings on a given property, the property will have to be using a contract containing the changes described in this proposal.


## Reference Implementation

An optional section that contains a reference/example implementation that people can use to assist in understanding or implementing this specification.  If the implementation is too large to reasonably be included inline, then add a link to a permanent URL where it can be found.


## Security Considerations

We shouldn't allow everyone to be a referrer. Otherwise, everyone could use his or her own address as a referrer to get referral rewards on their own bookings. Instead, this booking referral reward system is intended to be used as a permissioned affiliate marketing program (https://en.wikipedia.org/wiki/Affiliate_marketing) and the admitted affiliates/referrers should be expelled if abuse is noticed.