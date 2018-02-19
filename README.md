# Send Visit* Data Directly to predict.io (iOS Only)

> **NOTE** *Visit data means data generated solely by the [iOS Visit API](https://developer.apple.com/documentation/corelocation/clvisit), you must be sure that the data you capture and send to this endpoint *actually* originates from there.

You can send data directly to us at predict.io, skipping the requirement for installing our SDK for iOS & Android in your apps.

This solution can be useful if you already are capturing visit or location information from your users and would prefer sending it directly from your own servers rather than integrating an SDK to capture the same data you already are receiving.

## Visit Data Structure

### Example JSON

```json
{
  "device_data": {
    "advertising_id": "FDD3186B-637D-48C8-A388-B86997D44415",
    "app_id": "io.predict.waypoints.snapshot",
    "device_vendor": "Apple",
    "device_model": "iPhone10,6",
    "platform_version": "11.1",
    "locale": "de_DE"
  },
  "visit": {
    "arrived_at": "2017-11-08T14:48:31.099Z",
    "departed_at": "2017-11-08T14:48:31.099Z",
    "horizontal_accuracy": 5,
    "vertical_accuracy": 5,
    "latitude": 52.531702000000003,
    "longitude": 13.388479999999999
  }
}
```

### Device Data

| Key                | Description                              | Accepted Values                          |
| ------------------ | ---------------------------------------- | ---------------------------------------- |
| `advertising_id`   | Advertising ID if available on the the device. An empty or zeroed will be assumed to be an opt out from advertising. | `null` or `String` – e.g. ` FDD3186B-637D-48C8-A388-B86997D44415` |
| `app_id`           | Identifier of the app which generated the visit event. | `null` or `String` – e.g. `io.predict.ios.app` |
| `device_vendor`    | Name of the device manufacturer.         | `null` or `String` – e.g. `Apple`, `Samsung`, etc. |
| `device_model`     | Model of the device.                     | `null` or `String` – e.g. `iPhone X`, `Galaxy S8` |
| `platform_version` | OS version of the device platform.       | `null` or `String` – e.g. `11.1`, `7.0.1`, `8.0` |
| `locale`           | User's device locale.                    | `null` or `String` – e.g. `de_DE`, `en_US`, etc. |

### Visit Data

| Key                   | Description                              | Accepted Values                          |
| --------------------- | ---------------------------------------- | ---------------------------------------- |
| `arrived_at`          | ISO8601 formatted timestamp of when the device arrived. | `null` or `ISO8601 String` – e.g. ` 2017-11-08T14:48:31.099Z` |
| `departed_at`         | ISO8601 formatted timestamp of when the device departed. | `null` or `ISO8601 String` – e.g. ` 2017-11-08T14:48:31.099Z` |
| `horizontal_accuracy` | Horizontal accuracy of the event.        | `null` or `Double` – e.g. `12.75`        |
| `latitude`            | Latitude of the visit location.          | `Double` – e.g. ` 52.5317`               |
| `longitude`           | Longitude of the visit location.         | `Double` – e.g. ` 13.3884`               |

------

## How to Collect Visit Data? (iOS Only)

Visit data is collected using the [iOS Visit API](https://developer.apple.com/documentation/corelocation/clvisit), which is _background_ location functionality of [`CoreLocation`](https://developer.apple.com/documentation/corelocation). You must take the necessary steps to make sure that you have the required permissions in your app to ['Request Always Authorization'](https://developer.apple.com/documentation/corelocation/choosing_the_authorization_level_for_location_services/requesting_always_authorization).

With that you can follow Apple's documentation on ['Using the Visits Location Service'](https://developer.apple.com/documentation/corelocation/getting_the_user_s_location/using_the_visits_location_service) and with that data transform it into the JSON structure documented above.

> **NOTE** A `CLVisit` whose `arrivalDate` is `distantPast` or `departureDate` is `distantFuture` should **be ignored.**

