# SignArch
*SignArch* is an architectural description (AD) of the Android client of the [Signal messaging application](https://play.google.com/store/apps/details?id=org.thoughtcrime.securesms), or simply *Signal Android*, originally developed by Open Whisper Systems and now by its successor, [Signal Messenger](https://en.wikipedia.org/wiki/Signal_Messenger).

## Content of this AD

0. This [README](README.md) file, which contains an introduction summary of [Signal Android](#Signal-and-Signal-Android) and this [architectural description](#Purpose-and-Format-of-this-AD).
1. Introduction to Signal Android’s [development philosophy](1-introduction/concerns.md) and [stakeholders](1-introduction/stakeholders.md), as well as slides used to support two presentations ([first](1-introduction/Presentation_2019-02-27.pdf), [second](1-introduction/Presentation_2019-04-03.pdf)) of Signal Android's architecture
2. [Context View](2-context/context.md) providing an overview of the development and deployment context of Signal Android
3. [Functional View](3-functional/functional.md) introducing the major functional elements
4. [Information View](4-information/information.md) describing how information is handled *(this view does not need to be read after the Functional view)*

- [Appendices](appendices/): describing relevant background concepts about the [Android Framework](appendices/android.md) and [cryptography](appendices/cryptography.md).
- [AD-development](AD-development/): set of resources used during the development of this AD.

## Signal and Signal Android
Signal is a multi-platform messaging application for simple private communication. It conforms to high privacy and security standards, following the [privacy-by-design](http://carmelatroncoso.com/papers/Gurses-APC15.pdf) principle. However, it presents a user-friendly interface and handles high data throughput, so that privacy and security do not come at the cost of lower usability.

While Signal has a large ecosystem that includes client and server system for different platforms, and Signal's own encryption protocols, this AD focuses on the Android client only. As a part of a larger system, Signal Android needs to co-evolve with the Android Framework and remain up-to-date with state of the art cryptographic and communication protocols.

At the time of writing, Signal Android is a 100k LOC Java application with a large user base (over 10M installs on [Google Play](https://play.google.com/store/apps/details?id=org.thoughtcrime.securesms&hl=en)) and an active [development community](https://github.com/signalapp/Signal-Android/graphs/contributors) (over 175 contributors to the GitHub repository, with several commits per day, and an active [community forum](https://community.signalusers.org/)). It has been discussed in news websites such as [The Verge](https://www.theverge.com/2016/10/4/13161026/signal-subpoena-court-order-encryption-police-open-whisper), [Wired](https://www.wired.com/story/ditch-all-those-other-messaging-apps-heres-why-you-should-use-signal/), and [Electronic Frontier Foundation](https://www.eff.org/node/82654).

The code of this application is hosted on [GitHub](https://github.com/signalapp/Signal-Android).

## Purpose and Format of this AD

The purpose of this AD is to allow developers new to Signal to understand the general architecture of Signal Android, as well as important related concepts and principles used to inform the architecture.

The views presented in this AD follow the Context, Functional, and Information viewpoints described in [*Software Systems Architecture: Working with Stakeholders using Viewpoints and Perspectives*](https://www.viewpoints-and-perspectives.info/), 2nd edition, by Rozanski and Woods. This reference book also guided the content and format of the other parts of this AD.

This AD was developed by five students as part of a course on Software Architecture taught at McGill University, Canada, during the Winter 2019 term. The history of this AD may reflect its origin, and traces of previous stages are kept in the [AD-development](AD-development/) folder.

## AD Authors

**Main authors:**

 * Mathieu Nassif
 * Dong Wang
 * Maximilian Schiedermeier
 * Duan Li
 * Maksim Bober

**We thank the following people for their helpful feedback on this AD:**

* Prof. Martin P. Robillard (course instructor)
* Rez GodarzvandChegini (TA)
* Kaylee Kutschera (TA)
* Students of McGill's COMP 529 class of Winter 2019
