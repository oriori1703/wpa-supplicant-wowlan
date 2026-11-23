# wpa_supplicant WoWLAN test builds

Fedora packaging with upstream Hostap commit [`2633ca01fd48`](https://git.w1.fi/cgit/hostap/commit/?id=2633ca01fd4818b823d3190a5f1677a4e18d3e43) backported for [Fedora bug #2572081](https://bugzilla.redhat.com/show_bug.cgi?id=2572081). The patch passes the WPA3-SAE authentication suite to the Wi-Fi driver for GTK rekey offload during suspend.

The spec is based on Fedora Rawhide's `2.12-1` packaging. The only spec changes are the backport and the `.wowlan1` release suffix. COPR fetches the upstream tarball from `w1.fi` and verifies it against Fedora's `sources` checksum.

The [COPR project](https://copr.fedorainfracloud.org/coprs/oriori1703/wpa-supplicant-wowlan/) targets Fedora 44 and 45 on x86_64. This is an unofficial test package: keep the stock RPM available for rollback and install only while you have local access. Restarting `wpa_supplicant` can briefly disconnect Wi-Fi. Stop using this repository once your distribution ships the fix.
