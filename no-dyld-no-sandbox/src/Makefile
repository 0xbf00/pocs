# Adapt signing identity to locally available cert name
SIGNING_IDENTITY=Developer

unsandboxed-poc: unsandboxed-bin entitlements.xml
	@echo Building unsandboxed-poc
	cp unsandboxed-bin unsandboxed-poc
	codesign --force -s $(SIGNING_IDENTITY) --entitlements entitlements.xml unsandboxed-poc

clean:
	rm -f unsandboxed-poc