# Concerns

This file describes a concern and an architectural principle (with a consequent design decision) that guides the development of Signal Android.

## Concern: Privacy

**Privacy** is a cornerstone around which Signal Android is built, as their motto expresses [1]:

> Fast, simple, secure.
>
> Privacy that fits in your pocket.

The user's data should not be accessible without explicit authorization from the user.

More formally, an unauthorized third party with access to any consumer-grade technology, to Signal's servers, and to the history of the conversation between two users should not be able to access the users' unencrypted conversation or personal data under a reasonable amount of time (less than a few years).

The data affected by this concern include the content of conversations, videos, attachments, etc. However, surface level information, such as the frequency of messages between two users, is excluded from this concern, as hiding such level of information would come at a high cost on the usability of the application, its performance, or both.

## Architectural Principle: Data Minimization

Signal follows the architectural principle of **data minimization** [2]. This principle states that the different elements of a system should minimize the collection of data, the possibility of data collection, and the duration for which data is stored. It is achieved by minimizing collection, disclosure, linkability, centralization, replication, and retention of any user-related data.

Following this principle minimizes privacy risks and assumptions of trust placed on other entities. This principle directly targets the privacy concern described above.

This principle highlights issues in the management of [personally identifying information](https://en.wikipedia.org/wiki/Personal_data) (PII).

- Two communicating clients should have the absolutely minimal amount of information needed for the conversation to happen through Signal Android.
- Messages should be stored only as long as they are needed, and the user must be able to delete them.
- Minimizing centralization impacts the information that each entity (different clients, servers, etc.) will store, and how to limit the risk from a compromised part of the infrastructure.
- It limits the information that can be gathered for other purposes, such as targeted advertisement.

### Design decision

Signal Android encrypts all user communications along all the links in the communication path. The encrypted message is never decrypted in transit and the only recipient of the message is able to decrypt it. This is called [end-to-end encryption](../appendices/cryptography.md#End-to-end-encryption) (E2EE).

To guarantee E2EE, the public key infrastructure (PKI) should be handled by the endpoints, and the endpoints should be encrypted. Therefore, Signal Android should manage cryptographic keys and the data (including the keys) should not be stored unencrypted.

#### Cryptographic key infrastructure on endpoint

Signal Android implements code needed for management of public and private keys in [`org.thoughtcrime.securesms.crypto`](https://github.com/signalapp/Signal-Android/tree/master/src/org/thoughtcrime/securesms/crypto) package. This package is frequently used by other parts of the application for encrypting communication, storage, and [creation of new keys](https://github.com/signalapp/Signal-Android/blob/master/src/org/thoughtcrime/securesms/crypto/MasterSecretUtil.java). In fact, the most frequently used class is [`MasterSecret`](https://github.com/signalapp/Signal-Android/blob/master/src/org/thoughtcrime/securesms/crypto/MasterSecret.java) which is the data structure used to encrypt and decrypt user data. In particular, it wraps a 128-bit symmetric encryption key and a 160-bit symmetric MAC key.

Signal uses different cryptographic protocols and technologies for different tasks: communication, database file encryption/decryption, attachment encryption, and storage of keys. This is expected because the encryption of the file requires different API from the encryption of a short key. One needs to be encrypted in bulk while the other is short and has to be often retrieved.

#### Endpoint encryption
Signal Android an SQLite database, through [SQLCipher](https://www.zetetic.net/sqlcipher/design/), an open source library that provides transparent, secure 256-bit AES encryption for encryption of SQLite database files. SQLCipher itself uses encryption tools provided by popular encryption libraries, including [OpenSSL libcrypto](https://www.openssl.org/), [LibTomCrypt](https://www.libtom.net/), and [CommonCrypto](https://developer.apple.com/security/).

Database related code can be found at [`org.thoughtcrime.securesms.database`](https://github.com/signalapp/Signal-Android/tree/master/src/org/thoughtcrime/securesms/database). It consists of schemas for database files and the logic necessary for querying and encrypting  records.

#### Code Investigation
This section reveals some of the cryptographic infrastructure of Signal Android. *All commands are executed inside of [src/](https://github.com/signalapp/Signal-Android/tree/master/src) directory.*

###### Exploring database code
```
DatabaseFactory.java

 SmsDatabase
 MmsDatabase
 AttachmentDatabase
 MediaDatabase
 ThreadDatabase
 MmsSmsDatabase
 IdentityDatabase
 DraftDatabase
 PushDatabase
 GroupDatabase
 RecipientDatabase
 ContactsDatabase
 GroupReceiptDatabase
 OneTimePreKeyDatabase
 SignedPreKeyDatabase
 SessionDatabase
 SearchDatabase
```
*The information related to user communication, identity, searches, keys, sessions, and contacts are stored inside encrypted SQLite database files.*

###### Exploring cryptographic code

```
grep -R "org.thoughtcrime.securesms.crypto" | cut -d ':' -f2 | sort | uniq -c
      1 import org.thoughtcrime.securesms.crypto.AsymmetricMasterCipher;
      8 import org.thoughtcrime.securesms.crypto.AttachmentSecret;
      6 import org.thoughtcrime.securesms.crypto.AttachmentSecretProvider;
      5 import org.thoughtcrime.securesms.crypto.ClassicDecryptingPartInputStream;
      2 import org.thoughtcrime.securesms.crypto.DatabaseSecret;
      1 import org.thoughtcrime.securesms.crypto.DatabaseSecretProvider;
      5 import org.thoughtcrime.securesms.crypto.IdentityKeyParcelable;
     12 import org.thoughtcrime.securesms.crypto.IdentityKeyUtil;
      3 import org.thoughtcrime.securesms.crypto.InvalidPassphraseException;
      1 import org.thoughtcrime.securesms.crypto.KeyStoreHelper;
      2 import org.thoughtcrime.securesms.crypto.MasterCipher;
     25 import org.thoughtcrime.securesms.crypto.MasterSecret;
      8 import org.thoughtcrime.securesms.crypto.MasterSecretUtil;
      4 import org.thoughtcrime.securesms.crypto.ModernDecryptingPartInputStream;
      3 import org.thoughtcrime.securesms.crypto.ModernEncryptingPartOutputStream;
      5 import org.thoughtcrime.securesms.crypto.PreKeyUtil;
      1 import org.thoughtcrime.securesms.crypto.PRNGFixes;
      7 import org.thoughtcrime.securesms.crypto.ProfileKeyUtil;
      3 import org.thoughtcrime.securesms.crypto.SecurityEvent;
      3 import org.thoughtcrime.securesms.crypto.SessionUtil;
      3 import org.thoughtcrime.securesms.crypto.storage.SignalProtocolStoreImpl;
      3 import org.thoughtcrime.securesms.crypto.storage.TextSecureIdentityKeyStore;
      1 import org.thoughtcrime.securesms.crypto.storage.TextSecurePreKeyStore;
      3 import org.thoughtcrime.securesms.crypto.storage.TextSecureSessionStore;
     21 import org.thoughtcrime.securesms.crypto.UnidentifiedAccessUtil;
     23 package org.thoughtcrime.securesms.crypto;
      4 package org.thoughtcrime.securesms.crypto.storage;
```
*The crypto package is used frequently through the entire project.*

###### Exploring classes using the cryptographic functionalities

```
grep -R "org.thoughtcrime.securesms.crypto" | cut -d ':' -f1 | grep -v "org/thoughtcrime/securesms/crypto/"| sed "s/org\/thoughtcrime\/securesms\///" | uniq -c
      1 service/WebRtcCallService.java
      3 service/KeyCachingService.java
      5 providers/PersistentBlobProvider.java
      2 VerifyIdentityActivity.java
      1 WebRtcCallActivity.java
      5 RegistrationActivity.java
      1 preferences/AppProtectionPreferenceFragment.java
      1 PassphraseActivity.java
      2 DatabaseUpgradeActivity.java
      1 ConfirmIdentityDialog.java
      2 mms/SignalGlideModule.java
      1 dependencies/AxolotlStorageModule.java
      1 dependencies/SignalCommunicationModule.java
      1 push/SecurityEventListener.java
      3 PassphraseCreateActivity.java
      2 util/IdentityUtil.java
      1 util/DirectoryHelper.java
      1 util/VerifySpan.java
      1 database/loaders/DeviceListLoader.java
      5 database/DatabaseFactory.java
      5 database/helpers/ClassicOpenHelper.java
      5 database/helpers/SQLCipherMigrationHelper.java
      2 database/helpers/SQLCipherOpenHelper.java
      4 database/AttachmentDatabase.java
      1 CreateProfileActivity.java
      3 PassphraseChangeActivity.java
      2 backup/FullBackupImporter.java
      4 backup/FullBackupExporter.java
      1 ApplicationContext.java
      1 ConversationUpdateItem.java
      3 PassphrasePromptActivity.java
      1 BindableConversationListItem.java
      2 ConversationActivity.java
      1 RecipientPreferenceActivity.java
      2 DeviceActivity.java
      3 video/EncryptedMediaDataSource.java
      1 PassphraseRequiredActionBarActivity.java
      1 jobs/LocalBackupJob.java
      1 jobs/SmsSendJob.java
      1 jobs/MmsDownloadJob.java
      2 jobs/MultiDeviceBlockedUpdateJob.java
      1 jobs/SendDeliveryReceiptJob.java
      3 jobs/RefreshPreKeysJob.java
      1 jobs/SendReadReceiptJob.java
      1 jobs/AvatarDownloadJob.java
      1 jobs/RefreshAttributesJob.java
      1 jobs/RequestGroupInfoJob.java
      1 jobs/SendJob.java
      3 jobs/MultiDeviceProfileKeyUpdateJob.java
      2 jobs/MultiDeviceReadUpdateJob.java
      2 jobs/MultiDeviceContactUpdateJob.java
      1 jobs/RefreshUnidentifiedDeliveryAbilityJob.java
      1 jobs/AttachmentDownloadJob.java
      1 jobs/PushGroupSendJob.java
      3 jobs/CreateSignedPreKeyJob.java
      1 jobs/MultiDeviceVerifiedUpdateJob.java
      1 jobs/RotateProfileKeyJob.java
      1 jobs/MultiDeviceReadReceiptUpdateJob.java
      5 jobs/PushDecryptJob.java
      2 jobs/MultiDeviceGroupUpdateJob.java
      1 jobs/PushGroupUpdateJob.java
      1 jobs/TypingSendJob.java
      1 jobs/PushSendJob.java
      1 jobs/PushTextSendJob.java
      1 jobs/MultiDeviceConfigurationUpdateJob.java
      1 jobs/PushMediaSendJob.java
      1 jobs/RetrieveProfileJob.java
      2 jobs/CleanPreKeysJob.java
      1 jobs/SmsSentJob.java
      3 jobs/RotateSignedPreKeyJob.java
      1 logging/LogSecretProvider.java
```
*The crypto package is used in critical places in the application code such as: jobs, databases, push notifications, backup, and communication related classes.*

## End Notes
[1] As see on their website: https://signal.org/

[2] Seda Gurses, Carmela Troncoso, Claudia Diaz. "Engineering Privacy by Design," *Computers, Privacy & Data Protection*, 2011, vol. 14, no. 3, p. 25, 2011. Available online: https://software.imdea.org/~carmela.troncoso/papers/Gurses-CPDP11.pdf
