all: build/TestFairy-release.ipa

# build/TestFairy-adhoc.ipa 
# build/TestFairy-appstore.ipa

platforms/ios/build/device/TestFairy.app/TestFairy:
	cordova build ios --release --device

build/TestFairy-release.ipa: platforms/ios/build/device/TestFairy.app/TestFairy

	-rm -rf $@ platforms/ios/build/device/.package
	mkdir -p build platforms/ios/build/device/.package/Payload
	cp -R platforms/ios/build/device/TestFairy.app platforms/ios/build/device/.package/Payload
	codesign -v -f -i com.testfairy.app platforms/ios/build/device/.package/Payload/TestFairy.app
	(cd platforms/ios/build/device/.package; zip -rp9 ../../../../../$@ Payload)
	-rm -rf platforms/ios/build/device/.package

clean:
	-rm -rf ./build
	-rm -rf ./platforms/ios/build/
	-rm -rf ./platforms/ios/CordovaLib/build/CordovaLib.build/

