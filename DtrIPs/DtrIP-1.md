---
DTrIP: 1
title: Multiple Booking Data Providers
description: Disintermediates Dtravel as the sole provider of booking data for the on-chain booking contracts
author: [Perito Moreno](@PeritoM)
discussions-to: https://dtravelworkspace.slack.com/archives/C02H2KZDW2C/p1659422569494559 
status: Draft
category: Booking Contract Improvement
---

## Abstract

The current booking contract receives booking details (e.g. cancellation policy, amount paid, …) from the Dtravel backend. These booking details are signed by the Dtravel backend using its private key. The booking contract is programmed to verify this signature and to accept data only from the Dtravel backend.

We propose to generalize the booking contract by having a whitelist of multiple addresses, so that signed booking details from any of these addresses will be accepted by the contract. Therefore, any entity holding the private keys of these addresses will be able to provide booking data to the contract. We propose to allow the host to include more addresses in the whitelist and to remove them.


## Motivation

The goal of on-chain booking is to enable bookings without intermediaries (or, more correctly, with the blockchain and the smart contracts as the only intermediaries). But the current version of the booking contract requires intermediation by the Dtravel backend, since it is the only entity that may provide booking details to the contract.

In order to remain true to our goal, to our narrative to the community and to our promise to hosts and guests, we must fix this issue. One way to do this is by allowing the contracts to have multiple alternative providers of booking data.

Furthermore, the main potential of on-chain bookings will only be unleashed when the blockchain becomes the single source of truth for whether a property is booked or not. For this potential to be fully realized, it would be helpful to allow the PMSs to interact directly with the contract by becoming providers of booking details to the contract.

Ultimately, this simple improvement proposal is an initial step to allow Dtravel to progress from a direct booking platform to a booking protocol.


## Specification
_The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119._

- [ ] The booking contract must be extended with a whitelist of addresses whose signatures are accepted when verifying the provided booking details.
- [ ] The booking contract must have a new function that allows the host or its delegates to add new addresses to the whitelist.
- [ ] The booking contract must have a new function that allows the host or its delegates to remove addresses to the whitelist.
- [ ] Since there can be multiple booking data providers that are out-of-sync, the `book` function in the booking contract must be updated to check for availability. (Currently, the booking contract trusts the Dtravel backend to only call `book` on periods when the property is available.)


## Rationale

An alternative to this proposal would be to have the booking details stored directly in the contract, instead of being provided by a booking data provider in a signed message. This alternative would probably be ideal in the long-term, but the approach proposed here is simpler to implement given the current status.


## Backwards Compatibility

This proposal is fully backwards compatible. Properties with older booking contract versions would be able to continue operating normally, because the Dtravel backend would be able to make bookings in the same way independently of the version of the booking contract deployed for the property.


## Security Considerations

- Multiple booking data providers would increase the resilience of Dtravel as a protocol.
    - Currently, the Dtravel backend is a single point of potential failure.
    - In this sense, security would increase.
- Because the host will be able to remove booking data providers, an attacker who steals the private key of the host could remove all booking data providers and thus render the booking contract unusable.
    - However, in such an event, the attacker can already do much bigger damages anyway, such as stealing all funds from the host's wallet. A redeployment of the smart contract, using an uncompromised address from the host, would be the sensible solution.

