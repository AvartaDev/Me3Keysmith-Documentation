---
sidebar_position: 1
toc_max_heading_level: 4
title: Introduction
slug: /
---

## Summary

Keysmith is a NodeJS library for Dapps to seamlessly create wallets for use with the Me3 ecosystem. By integrating with Keysmith, wallets are created and stored on the end user's Google Drive.

These wallets are accessed only via the user's explicit authorization via Google <abbr title="single sign on">SSO</abbr>. This is a one-click approval process - Google opens a pop-up which requests for the user's approval. It is written in Java with Spring Boot.

Should the user not be signed on their Google account, this is simply one additional click - Google prompts the user to sign in via SSO.

## Is Keysmith non-custodial?

Keysmith simply provides an easy-to-use way for Dapps to create wallets, in a manner that has superior UI/UX to the end-user. Whether it is implemented as a custodial solution (where the Dapp has oversight over the user's private keys) or non-custodial (where the Dapp has no such oversight) is up to the Dapp's implementation of the library.

In all situations, Me3 does not have the ability to view any information regarding user's wallets.

## What can I do with wallets created via Keysmith?

Wallets created by Keysmith are automatically compatible with the rest of Me3's ecosystems, such as partner DApps or the mobile wallet, allowing one-click access to Web3.0.

## What can I do with Keysmith?

Keysmith currently allows you to do two things:

1. Create wallets on the user's Google Drive, and access them via Google SSO
1. Sign EVM transactions based on the EVM wallet created on the user's Google Drive

We are working to implement more features, so stay tuned to this page!
