# snipe-sdk-android

The `SnipeSdk` library provides functionalities for interacting with the Snipe API.

The SnipeSdk library provides a seamless integration of Snipe functionality into your Android application through an AAR (Android Archive) file and the use of a flat directory. Follow these steps to install SnipeSdk using the AAR file and configure the flat directory approach.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
  - [Initialization](#initialization)
  - [Sign Up](#sign-up)
  - [Get Coin Data](#get-coin-data)
  - [Track Event](#track-event)


## Installation

To use the `SnipeSdk` library in your Android project, you can follow these steps:
## Steps

1. **Download the AAR File:**

   Obtain the SnipeSdk AAR file from a reliable source. This AAR file encapsulates the compiled library and its resources.

2. **Add the AAR File to the 'libs' Folder:**

   - In the root directory of your Android project, create a new folder named `libs` if it doesn't already exist.
   - Copy the downloaded SnipeSdk AAR file into the newly created `libs` folder.

3. **Configure Flat Directory in settings.gradle:**

   - Open the `settings.gradle` file located in the root directory of your Android project.
   - Inside the `repositories` section, add the following code to configure the flat directory:

     ```gradle
     repositories {
         flatDir {
             dirs 'libs'
         }
         // Other repositories...
     }
     ```

4. **Modify the Build Gradle File (app module):**

   - Open the `build.gradle` file of your app module (usually named `app`).
   - Inside the `dependencies` block, add the following code to include the SnipeSdk AAR file:

     ```gradle
     dependencies {
         implementation fileTree(dir: 'libs', includes: ['*.jar', '*.aar'])
         implementation(name: 'snipesdk-release', ext: 'aar')
         // Other dependencies...
     }
     ```

5. **Sync Gradle:**

   After modifying the `settings.gradle` and app module's `build.gradle` files, click on the "Sync Now" prompt that appears in Android Studio. This action syncs your project and makes the SnipeSdk library available for use.


## Usage

### Initialization

Before using any functions provided by the `SnipeSdk`, you need to initialize it with your API key.

```kotlin
SnipeSdk.init("YOUR_API_KEY")
```

### Sign Up

The `signUp` function in the `SnipeSdk` library allows you to perform a sign-up operation by creating a document in the Snipe database and returning the associated Snipe ID.

#### Parameters

- `hash` (Type: `String`): The input hash value that will be used to perform the sign-up operation.

#### Return Value

- `String`: The Snipe ID associated with the created document in the Snipe database.

#### Usage

```kotlin
val hash = "your_hash_value"
val snipeSdk = SnipeSdk.get()
val signUpResponse = snipeSdk.signUp(hash)
```

### Get Coin Data

The `getCoinData` function in the `SnipeSdk` library allows you to retrieve coin data associated with a specific Snipe ID from the Snipe database.

#### Parameters

- `snipeId` (Type: `String`): The Snipe ID for which you want to retrieve the coin data.

#### Return Value

- `List<Map<String, Any>>`: A list of maps containing coin data. Each map represents a coin with its associated attributes.

#### Usage

```kotlin
val snipeId = "your_snipe_id"
val snipeSdk = SnipeSdk.get()
val coinData = snipeSdk.getCoinData(snipeId)
```

### Track Event


The `trackEvent` function in the `SnipeSdk` library allows you to track and trigger events in the Snipe system. You can use this function to record events with optional transaction amount and partial percentage details.

#### Parameters

- `eventId` (Type: `String`): The ID of the event you want to track.
- `transactionAmount` (Type: `Int?`, Default: `null`): The transaction amount associated with the event (optional).
- `partialPercentage` (Type: `Int?`, Default: `null`): The partial percentage of the event (optional).

#### Return Value

This function does not have a return value. It triggers an event in the Snipe system.

#### Usage

```kotlin
val eventId = "your_event_id"
val transactionAmount = 100
val partialPercentage = 50
val snipeSdk = SnipeSdk.get()
snipeSdk.trackEvent(eventId, transactionAmount, partialPercentage)
```
