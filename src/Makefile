all: release adhoc 

adhoc: build/TestFairy-adhoc.ipa 

release: build/TestFairy-release.ipa

# appstore: build/TestFairy-appstore.ipa

platforms/ios/build/device/TestFairy.app/TestFairy:
	cordova build ios --release --device
	xcrun -sdk iphoneos lipo -info ./platforms/ios/build/device/TestFairy.app/TestFairy | grep "armv7 armv7s arm64" 

build/TestFairy-adhoc.ipa: platforms/ios/build/device/TestFairy.app/TestFairy
	-rm -f $@
	-rm -rf platforms/ios/build/device/.package
	mkdir -p build platforms/ios/build/device/.package/Payload
	cp -R platforms/ios/build/device/TestFairy.app platforms/ios/build/device/.package/Payload
	cp ../scripts/certs/cert-adhoc.mobileprovision platforms/ios/build/device/.package/Payload/TestFairy.app/embedded.mobileprovision
	codesign -v -f -i com.testfairy.app -s "iPhone Distribution: TestFairy LTD (8Z9PUDZ69F)" platforms/ios/build/device/.package/Payload/TestFairy.app
	(cd platforms/ios/build/device/.package; zip -rp9 ../../../../../$@ Payload)
	-rm -rf platforms/ios/build/device/.package

build/TestFairy-release.ipa: platforms/ios/build/device/TestFairy.app/TestFairy
	-rm -f $@ 
	-rm -rf platforms/ios/build/device/.package
	mkdir -p build platforms/ios/build/device/.package/Payload
	cp -R platforms/ios/build/device/TestFairy.app platforms/ios/build/device/.package/Payload
	codesign -v -f -i com.testfairy.app platforms/ios/build/device/.package/Payload/TestFairy.app
	(cd platforms/ios/build/device/.package; zip -rp9 ../../../../../$@ Payload)
	-rm -rf platforms/ios/build/device/.package

clean:
	-rm -rf ./build
	-rm -rf ./platforms/ios/build/
	-rm -rf ./platforms/ios/CordovaLib/build/CordovaLib.build/

