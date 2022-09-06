---
DTrIP: <Use the smallest integer not yet used by any other DTrIP>
title: <The DTrIP title is a few words, not a complete sentence>
description: <Description is one full (short) sentence>
author: <a comma separated list of the author's or authors' name + GitHub username (in parenthesis), or name and email (in angle brackets).  Example, FirstName LastName (@GitHubUsername), FirstName LastName <foo@bar.com>, FirstName (@GitHubUsername) and GitHubUsername (@GitHubUsername)>
discussions-to: <URL>
status: Draft
category:
requires (*optional): <DTrIP number(s)>
---

This is the suggested template for new DTrIPs.

Note that a DTrIP number will be assigned by an editor. When opening a pull request to submit your DTrIP, please use an abbreviated title in the filename, `DTrIP-draft_title_abbrev.md`.

The title should be 44 characters or less. It should not contain the DTrIP number. 

## Abstract
Abstract is a multi-sentence (short paragraph) technical summary. This should be a very terse and human-readable version of the specification section. Someone should be able to read only the abstract to get the gist of what this specification does.

## Motivation
The motivation section should describe the "why" of this DTrIP. What problem does it solve? Why should someone want to implement this standard? What benefit does it provide to the Dtravel ecosystem? What use cases does this DTrIP address?

## Specification
The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119.

The technical specification should describe the syntax and semantics of any new feature. The specification should be detailed enough to allow competing, interoperable implementations on top of the Dtravel protocol.

## Rationale
The rationale fleshes out the specification by describing what motivated the design and why particular design decisions were made. It should describe alternatative designs that were considered and related work.

## Backwards Compatibility
All DTrIPs that introduce backwards incompatibilities must include a section describing these incompatibilities and their severity. The DTrIP must explain how the author proposes to deal with these incompatibilities.

## Reference Implementation
An optional section that contains a reference/example implementation that people can use to assist in understanding or implementing this specification.  If the implementation is too large to reasonably be included inline, then add a link to a permanent URL where it can be found.

## Security Considerations
All DTrIPs must contain a section that discusses the security implications/considerations relevant to the proposed change. Include information that might be important for security discussions, surfaces risks and can be used throughout the life cycle of the proposal. E.g. include security-relevant design decisions, concerns, important discussions, implementation-specific guidance and pitfalls, an outline of threats and risks and how they are being addressed. DTrIP submissions missing the "Security Considerations" section will be rejected. An DTrIP cannot proceed to status "Final" without a Security Considerations discussion deemed sufficient by the reviewers.