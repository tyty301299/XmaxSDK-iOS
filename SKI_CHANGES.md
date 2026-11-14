Source: https://github.com/Xmax-AI/XmaxSDK-iOS
Revision: d4c9c3340a0095370efdd163ae8c85e6c2c8c594
License: MIT (see LICENSE).

Remote fork used by SKI for reproducible iOS builds. Binary dependencies are fetched by SwiftPM.
Local fix: AgoraRtcRoom.awaitPendingMessages explicitly returns self.sender from the lock closure to avoid shadowing the local sender binding (Swift compiler error).
When upgrading, check whether upstream includes this fix and rerun the device build.

RtcManager.initialize explicitly binds self.initialization and captures self.engineManager to avoid a Swift 6.3.2 ClosureLifetimeFixup compiler crash from shadowed bindings.

StreamController explicitly weak-captures self in the cancellation handler, avoiding a mutable outer weak capture across concurrent closures.

StorageManager uses QCloudCOSXMLEndPoint for custom literal endpoints. The abstract QCloudEndPoint throws an Objective-C exception in serverURLWithBucket:appID:regionName: during image upload (confirmed in device crash report 2026-11-14 14:15).
