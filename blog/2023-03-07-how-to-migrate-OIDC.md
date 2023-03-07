---
slug: How to use OIDC
title: How to use OIDC
authors: [guangzheng, tianzhen]
tags: [odic, oauth2]
---

his post is the next in a series of posts on authentication in ASP.NET Core. In the previous post we showed how you can use the OAuth 2.0 protocol to provide 'Login via Facebook' functionality to your website.

While a common approach, there are a number of issues with using OAuth as an authentication protocol, rather than the authorisation protocol it was designed to be.

Open ID Connect adds an additional layer on top of the OAuth protocol that solves a number of these problems. In this post we take a look at the differences between OpenID Connect and OAuth, how to use Open ID Connect in your ASP.NET Core application, and how to register your application with an OpenID Connect provider (in this case, Google).

What is OpenID Connect?
OpenID Connect is a simple identity layer that works over the top of OAuth 2.0. It uses the same underlying REST protocol, but adds consistency and additional security on top of the OAuth protocol.

It is also worth noting that OpenID Connect is a very different protocol to OpenID. The later was an XML based protocol, which follows similar approaches and goals to OpenID Connect but in a less developer-friendly way.