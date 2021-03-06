---
title: Authentication and user identity
description: Universal Windows Platform (UWP) apps have several options for user authentication, ranging from simple single sign-on (SSO) using Web authentication broker to highly secure two-factor authentication.
ms.assetid: 53E36DDC-200A-4850-AAF0-07ECA3662BB9
---

# Authentication and user identity


\[ Updated for UWP apps on Windows 10. For Windows 8.x articles, see the [archive](http://go.microsoft.com/fwlink/p/?linkid=619132) \]

Universal Windows Platform (UWP) apps have several options for user authentication, ranging from simple single sign-on (SSO) using [Web authentication broker](web-authentication-broker.md) to highly secure two-factor authentication.

For regular app connections to third-party identity provider services, such as Facebook, Twitter, Flickr, and so on, use the [Web authentication broker](web-authentication-broker.md). For added convenience, use [Credential Locker](credential-locker.md) to save and roam the user's login information.

Enterprises using Windows 10 should strongly consider using [Microsoft Passport and Windows Hello](microsoft-passport.md), which enables highly secure two-factor authentication. If using Microsoft Passport is not possible,[Smart cards](smart-cards.md) and [Fingerprint biometrics](fingerprint-biometrics.md) can add an additional layer of security.

| Topic                                                                                 | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|---------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Microsoft Passport and Windows Hello](microsoft-passport.md)                         | Microsoft Passport and Windows Hello replaces passwords with strong two-factor authentication (2FA) by verifying existing credentials and by creating a device-specific credential that a biometric or PIN-based user gesture protects. This combination effectively replaces physical and virtual smart cards as well as reusable passwords for logon and access control.                                                                                                                                                                              |
| [Create a Microsoft Passport login app](microsoft-passport-login.md)                  | Part 1 of a complete walkthrough on how to create a Windows 10 UWP (Universal Windows Platform) app that uses Microsoft Passport as an alternative to traditional username and password authentication systems.                                                                                                                                                                                                                                                                                                                                         |
| [Create a Microsoft Passport login service](microsoft-passport-login-auth-service.md) | Part 2 of a complete walkthrough on how to use Microsoft Passport as an alternative to traditional username and password authentication systems in Windows 10 UWP (Universal Windows platform) apps.                                                                                                                                                                                                                                                                                                                                                    |
| [Credential Locker](credential-locker.md)                                             | Credential Locker is a convenient and secure way to store user credentials that your app uses to connect to services like media, social networking, and so on. You can store a user's userid and password in the Credential Locker, and then automatically log them on to services when they use your app. Credentials stored in the Credential Locker automatically roam with a users's Microsoft Account.                                                                                                                                             |
| [Web authentication broker](web-authentication-broker.md)                             | Web authentication broker supports the OAuth and OpenID internet authentication protocols, so you can integrate your app with a web service that provides user authentication. This allows you to utilize user identity in your apps from services such as Facebook, Flickr, Google, and Twitter. You can also use the web authentication broker to enable single sign-on (SSO) for multiple internet authenticated apps.                                                                                                                               |
| [Fingerprint biometrics](fingerprint-biometrics.md)                                   | Including a request for fingerprint authentication when the user must consent to a particular action increases the security of your app. For example, you could require fingerprint authentication before authorizing an in-app purchase, or access to restricted resources. Fingerprint authentication is managed using the [UserConsentVerifier](https://msdn.microsoft.com/library/windows/apps/dn279134) class in the [Windows.Security.Credentials.UI](https://msdn.microsoft.com/library/windows/apps/hh701356) namespace.                        |
| [Smart cards](smart-cards.md)                                                         | Smart cards and virtual smart cards provide a high level of authentication for your app. You can use the APIs in the [Windows.Devices.SmartCards](https://msdn.microsoft.com/library/windows/apps/dn263949) namespace to authenticate a user using a smart card, gather information about smart card devices, and manage smart card devices, such as requesting a PIN reset. You can also create Trusted Platform Module (TPM) Virtual Smart Cards that provide smart card-level authentication without requiring a physical smart card from your user. |
| [Shared certificates](share-certificates.md)                                          | Certificate authentication provides a high level of trust when authenticating a user. Apps that require secure authentication beyond a userid and password combination can use certificates for authentication.                                                                                                                                                                                                                                                                                                                                         |
 

 

 






<!--HONumber=May16_HO4-->


