SHELL := /bin/bash
.SHELLFLAGS := -euo pipefail -c
spec ?= wpa_supplicant.spec
outdir ?= .

.PHONY: srpm
srpm:
	@src=$$(awk '/^SHA512 / { sub(/^SHA512 \(/, ""); sub(/\) = .*$$/, ""); print }' sources); \
	sum=$$(awk '/^SHA512 / { print $$NF }' sources); \
	test -n "$$src" && test -n "$$sum"; \
	tmp=$$(mktemp -d); trap 'rm -rf -- "$$tmp"' EXIT; \
	curl -fLsS --retry 3 --max-time 120 "https://w1.fi/releases/$$src" -o "$$tmp/$$src"; \
	printf '%s  %s\n' "$$sum" "$$tmp/$$src" | sha512sum -c -; \
	cp -- *.patch wpa_supplicant.conf wpa_supplicant.service wpa_supplicant.sysconfig wpa_supplicant.logrotate "$$tmp/"; \
	mkdir -p -- "$(outdir)"; \
	rpmbuild -bs --define "_sourcedir $$tmp" --define "_srcrpmdir $(abspath $(outdir))" "$(spec)"
