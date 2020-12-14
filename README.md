# Guide to customize jitsi-meet-sdk

## Generation of ios sdk from jitsi-meet

1. Install all dependencies

```
npm install
```
2. Generate sdk with following command

```
./android/scripts/release-sdk.sh target_path_of_android_sdk
```

After finish this command, you will be able to see a sdk for android in specific path.

## Generation of android sdk from jitsi-meet

1. Create directory("jitsi-meet-ios-sdk-releases") in the same level of jitsi-meet project.
2. Install all dependencies

```
npm install
```
3. Generate sdk with following command

```
./ios/scripts/release-sdk.sh
```

After finish this command, you will be able to see a sdk for android in "jitsi-meet-ios-sdk-releases" folder.


## react-native-jitsi-meet configure with generated sdks(android, ios)

### Android sdk configure

- Copy sdk folder and past it to react-native-jitsi-meet/android folder.
- Rename the folder to "jitsi_sdk"


### iOS sdk configure

- Copy "JitsiMeet.framework" and "WebRTC.framework" folder for arm64 from generate ios sdk.
- Paste them to jitsi_ios_sdk repository and submit it to github.

## How to use customized react-native-jitsi-eet

1. In main project folder, add react-native-jitsi-meet library to the project.

```
yarn add "git+https://github.com/RistoBIn/react-native-jitsi-meet.git"
```
2. Add following commands in Podfile

```
pod "JitsiMeetSDK", :git => "https://github.com/RistoBIn/jitsi_ios_sdk.git"
```

```
post_install do |installer|
	installer.pods_project.targets.each do |target|
		if target.name == 'react-native-jitsi-meet'
			target.build_configurations.each do |config|
				config.build_settings['FRAMEWORK_SEARCH_PATHS'] ||= "${PODS_ROOT}/JitsiMeetSDK/Frameworks"
			end
		end
	end
end
```


3. Add following command in android/build.gradle

```
allprojects {
	repositories {
		maven{
			url("$rootDir/../node_modules/react-native-jitsi-meet/android/jitsi_sdk")
		}
	}
}
```
