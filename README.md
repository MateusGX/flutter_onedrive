## Features

* Download files from onedrive
* Upload files to onedrive

## References
Read below documents before you start using this library:
* https://docs.microsoft.com/en-us/onedrive/developer/rest-api/getting-started/app-registration?view=odsp-graph-online
* https://docs.microsoft.com/en-us/onedrive/developer/rest-api/getting-started/msa-oauth?view=odsp-graph-online
* https://github.com/flutter/plugins/tree/master/packages/url_launcher/url_launcher

## Getting started

```dart
flutter public add fixed_flutter_onedrive
```

```dart
import 'package:fixed_flutter_onedrive/fixed_flutter_onedrive.dart';
```

## Usage

```dart
final onedrive = OneDrive(callbackSchema: "your callback schema", clientID: "your client id");
return FutureBuilder(
  future: onedrive.isConnected(),
  builder: (BuildContext context, AsyncSnapshot<dynamic> snapshot) {
    if (!snapshot.hasData) {
      return const Center(child: CircularProgressIndicator());
    }
    if (snapshot.data ?? false) {
      // Has connected
      return const Text("Connected");
    } else {
      // Hasn't connected
      return MaterialButton(
        child: const Text("Connect"),
        onPressed: () async {
          final success = await onedrive.connect();
          if (success) {
            // Download files
            final txtBytes = await onedrive.pull("/xxx/xxx.txt");
            // Upload files
            await onedrive.push(txtBytes!, "/xxx/xxx.txt");
          }
        },
      );
    }
  },
);
```
