v0.42
=====

- !115 - Fix compilation on win32 with EGL
- !114 - spice-widget: fix hotspot position on Wayland/HiDPI
- !112 - meson: Allow building on a Wayland-only environment
- !110 - usb-backend: Fix devices not being enumerated
- !108 - spicy: Add keyboard shortcuts for copy/paste sync
- Require meson >= 0.56

v0.41
=====

- !100 - meson: move cairo dependency to GTK build only
- !102 - coroutine: add support for libucontext
- !105 - build against phodav-3.0/soup-3.0
- fix openssl 3.0 warnings
- meson: fix invalid use of subproject()

v0.40
=====

- Fix usbid parsing regression introduced in !78 (v0.39)
- !91 - Fix crash with division by 0 [rhbz#1941627]
- !97 - #157 - Fix detecting pyparsing module
- Add API to allocate SpiceUsbDevice (for Android)
  spice_usb_device_manager_allocate_device_for_file_descriptor()
- !93 - #137 - add support for TLS-SNI
- !92 - Support USB emulation for MacOS
- !96 - Support side mouse buttons
- !85 - #75 - add spice_display_keyboard_ungrab()
- !81 - GL fix warning fix and improve scanout logic
- !84 - Fix leak and warnings in gstaudio and spicy
- !86, !87, !90 - Several introspection fixes and improvements

[rhbz#1941627]: https://bugzilla.redhat.com/show_bug.cgi?id=1941627

v0.39
=====

- !33 - Remove PulseAudio backend
- !34 - Remove support to CELT codec
- !42 - Drop capabilities from usb-acl-helper binary
- !45 - #123 - Install ACL helper in libexec directory
- !48 - Add support to Wayland mouse in server mode
- !49 - #126 - Read all SASL buffer
- !54 - Add Copy & Paste support over Webdav
- !58 - Improve input and display on HiDPI displays
- !64 - Add support for Physical size display
- !69 - Fix leak on Display's surface
- !74 - Fix read overflow on (not seamless) migration code
- !75 - Fix usb redirect on connect, see [rhbz#1874740]
- !77 - Fixes buffer overflow in QUIC [CVE-2020-14355]
- Require polkit >= 0.101
- Require meson >= 0.53
- Require glib-2.0 >= 2.52

[rhbz#1874740]: https://bugzilla.redhat.com/show_bug.cgi?id=1874740
[CVE-2020-14355]: https://bugzilla.redhat.com/show_bug.cgi?id=1885566

v0.38
=====

- #108 - Add CD/DVD redirection, to allow mounting ISO images from client.
- #99 - Fix display scaling with EGL and HiDPI monitors
- #19 - Fix display corruption on HiDPI
- #82 - Various clipboard fixes & improvements, related to host/guest races &
  cltipboard managers
- [rhbz#1720532] - Fix buffer overflow on sending data with shared-folders
- [rhbz#1695618] - Fix hang over failed migration
- API: add spice_display_channel_change_preferred_video_codec_types()
- Several usbredir related fixes and code improvements
- Several video stream related fixes and code improvements
- Several shared-folder related fixes and code improvements
- file-xfer: fix stuck transfer while transfering multiple big files at once
- file-xfer: fix possible crash on Windows
- Migration: Fix metadata swap of channels
- build-sys: remove autotools (transition to meson completed)
- Require spice-protocol >= 0.14.1
- Require libusb >= 1.0.21
- Translations:
 - Update Italian
 - Add Russian

[rhbz#1720532]: https://bugzilla.redhat.com/show_bug.cgi?id=1720532
[rhbz#1695618]: https://bugzilla.redhat.com/show_bug.cgi?id=1695618

v0.37
=====

- Deprecated: SpiceMainChannel:color-depth and SpiceSession::color-depth see
  ([rhbz#1543538] and [rhbz#1350853]).
- Fix race condition on keyboard modifiers
- Fix cursor on Wayland: Fixes hidden cursor #83
- Fix clipboard on X11: avoid request client clipboard data when is known that
  there is no data.
- Improve code around usb redirection feature
- Fix on usb redirection: Don't add same device twice
- Fix on smartcard: Warn if multiple readers are detected
- Add instrumentation for frame and queue statistics of SpiceDisplay using
  [Recorder] library
- Fix Warnings with GStreamer >= 1.14 on video decoding due setting buffer's PTS
- Fix some Critical warnings when build without GNOME desktop integration
- Fix Criticals when no primary monitor is set
- Documentation fixes
- Added optional dependency: [Recorder]
- Require GStreamer >= 1.10 (optional)
- Require usbredir >= 0.7.1 (optional)
- Translations:
  - Added Czech
  - Fix Italian

[Recorder]: https://github.com/c3d/recorder
[rhbz#1543538]: https://bugzilla.redhat.com/show_bug.cgi?id=1543538
[rhbz#1350853]: https://bugzilla.redhat.com/show_bug.cgi?id=1350853

v0.36
=====

- Add meson build: autotools will be removed in a future release
- Deprecate PulseAudio backend: it will be removed in a future
  release, please use GStreamer instead and report issues
- Add H265 stream support (requires GStreamer support)
- Add SpiceQmpPort helper to interact with QEMU monitor over a Spice port
- Display a message if EGL support is required (with dmabuf local rendering)
- Many GstVideoOverlay improvements
- Smooth-scrolling improvements
- Fix accumulating decoded frames with GStreamer
- Fix reconnection handling
- Fix small memory leaks due to bad refcount of images in the cache
- Fix build for newer LibreSSL 2.7
- Fix a crash on Windows with libusb 1.0.22 when UsbDk is not installed
- Require GStreamer >= 1.0 (no longer optional)
- Require spice-protocol >= 0.12.15
- Require json-glib >= 1.0
- Require Gtk+ >= 3.22 (optional)
- Require usbredir >= 0.5 (optional)
- Require libusb >= 1.0.16 (optional)
- Require libcacard >= 2.5.1 (optional)
- Require lz4 >= 1.7.3 (optional)

v0.35
=====

- TLS v1.0 was disabled (rhbz#1521053)
- New SpiceSession::disconnected signal
- Use GstVideoOverlay if possible to render directly on Gstreamer's sink element
- Handling smooth-scroll for scroll events on touchpads in Wayland
- CELT codec is disabled by default but configure will error out if detects that
  its headers are available unless --enable-celt051/--disable-051 is used.
- Glib requirement bumped to 2.46
- Spice-protocol bumped to 0.12.14
- The spice-controller library was removed
- Fix migration regression introduced in v0.34 (rhbz#1558043)
- Fix connecting from big endian machine including SASL authentication
- Webdav: Fix some runtime warnings
- Introspection: Fixes for SpicePortChannel, SpiceDisplayChannel,
  SpiceRecordChannel, SpiceInputsChannel, SpiceMainChannel
- Enable ACL support on FreeBSD (fdo#104525)
- win32: Convert locale dir from UTF-8 to local encoding
- Fix width computation for palette images (rhbz#1508847)
- Introduction of spice+tls:// URI format to tls all channels
- Fix keycodes on Xwayland (rhbz#1479682)
- Memory leak fixes, new tests

v0.34
=====

- NOTE: this is the last release with the spice-controller library
- add VP9 codec support
- API: add spice_display_change_preferred_video_codec_type()
- API: add new SpiceCursorChannel:cursor property, deprecate "cursor-set" signal
- API: spice_audio_new() is no longer in public header (it was deprecated
  for a long while)
- fix clipboard crash and other regressions from 0.33
- report invalid or stopped streams to the server
- use playbin instead of decodebin with gstreamer > 1.9
- support GST_DEBUG_BIN_TO_DOT_FILE debug
- deprecate a few esoteric options from --spice group:
  --spice-color-depth, --spice-cache-size, --spice-glz-window-size used
  mainly for development. They may be available with spicy in the future.
- win32: handle failures when starting win-usb manager
- win32: removed windows usb-clerk support, replaced by UsbDk
- win32: fix alt-tab & grab issues
- spicy learned to tweak codec preference, cancel transfer, and resize
  precisely for debugging purposes
- use keycodemapdb submodule, drop perl(Text::CSV) dependency
- file-xfer: fix bad filename encoding
- file-xfer: handle new error kind
- build-sys fixes for macos
- replace some deprecated gtk code
- memory leak fixes, new tests

v0.33
=====

- lz4 compression of USB channel
- keyboard: pause key fixes, set keypress-delay to 0 on local socket
- mouse: fix pointer grabbing in server mode
- clipboard: fix copying text from old application without UTF8_STRING
  target (motif)
- file-xfer changes: grouping all transferred files per operation
- new spice_file_transfer_task_get_{total_bytes,transferred_bytes} API
  and associated properties
- new SpiceChannel:socket property
- fix rendering issues with CSD on Windows
- fix gettext support, some translations updates
- fix display refresh issue on f25 after resize (init egl only when
  required)
- many leaks and races fixes, new tests

v0.32
=====

libspice-client-gtk API/ABI break: library soname/version has been
bumped, and deprecated symbols have been removed.  In practice, most
of the API (in particular for language bindings) should be unchanged.

- drop gtk+ 2.0 support
- require gtk+ >= 3.12 and glib >= 2.36
- add GStreamer as a backend for mjpeg, vp8 & h264 decoding
  This allows the upcoming Spice server release to send video
  regions with better codecs.
- a number of spice-gtk structures are now private
- spice-gtk widget is no longer a GtkDrawingArea but an opaque type
  with only guarantee to be a GtkWidget
- virgl: use GtkGlArea if possible (on wayland only atm)
- virgl: various fixes (multiple display, resize, canvas-less support)
- win-usbredir: use UsbDk backend when available and various
  improvements
- ensure that dnd file copy get cancelled
- some JP and KR keyboard handling fixes on Windows
- fix SASL GSSAPI
- fix ipv6 proxy address handling
- allow smaller widget with scaling enabled
- add spice_main_request_mouse_mode() to request mouse mode
- add SpiceGtkSession:sync-modifiers to change modifiers sync behaviour
- various video decoding improvements
- use GTask instead of GSimpleAsyncResult
- misc bindings, leaks, warnings, and spelling fixes

v0.31
=====

- NOTE: this is the last release to support gtk+ 2.0
- add local GL scanout support for virtio-gpu/virgl guests
- new file-transfer API, to be able to monitor transfers etc
- new spice_display_change_preferred_compression() API
- better authentication error reports
- usbredir: drop isoc packets on low bandwidth (rhbz#1264156)
- usbredir: add counter of free channels (rhbz#1298772)
- add a toplevel include header spice-client-gtk.h
- grab keyboard based on session focus (rhbz#1275231)
- don't print error message on successful file transfer (rhbz#1265562)
- allow simultaneous support for Pulse and GStreamer audio
- remove GSlice usage
- some BE endianness fixes
- misc leak and use after-free fixes
- documentation fixes

v0.30
=====
- spice-protocol is no longer bundled with spice-gtk. Requires
  spice-protocol >= 0.12.10
- Handle single headed monitors that have a non-zero x, y config
- various small improvements to 'spicy' test application
- Fix build with automake < 1.13
- various bug fixes and improvements
- New API:
  - spice_main_update_display_enabled()
  - Add SpiceSession::preferred-compression property and
    --spice-preferred-compression commandline switch (requires a
    yet-to-be-released version of spice server)
- ability to set the SpiceDisplay::keypress-delay property via a new
  SPICE_KEYPRESS_DELAY environment variable

v0.29
=====

- sync guest audio volume with client volume
- use stream volume for PulseAudio source
- on Windows, fail early during initialization if the usbclerk service
  can't be reached
- fix audio and usb managers to work with client provided fds
- many crasher and bug fixes

v0.28
=====

- webdav improvements:
 - no longer spawn a server thread
 - no longer use local TCP sockets & port
 - provides read-only mode with SpiceSession:share-dir-ro
 - requires libphodav-2.0 glib-2.0 >= 2.43.90 libsoup-2.4 >= 2.49.91
- drop gstreamer 0.10 in favour of 1.0
- add spice+unix://path connection support
- accept URI with empty parameters value,
  such as spice://localhost?port=5900&tls-port=
- fixed lz4 support
- silence some harmless warnings
- misc API documentation improvements
- switch-host migration fixes
- learn to build --without-gtk
- bugs and regressions fixes

v0.27
=====

- add GStreamer 1.0 audio support
- add LZ4 compression algorithm support
- learn to release the keyboard grab on release keys pressed (ctrl+alt
  by default), to let alt+f4/alt-tab and others for client side
- session and channels life-cycle changes: a channel will no longer
  hold a reference after session disconnection
- migration fixes, fail early on client provided fds (this is left to
  solve in the future)
- fix support for Gtk+ 3.0 on Windows
- clipboard size fixes
- server-side pointer drawing on grab
- new APIs:
  spice_usb_device_get_libusb_device()
  spice_session_is_for_migration()
- build-sys improvements

v0.26
=====

- allow transferring multiple files at once with dnd
- avoid guest-side fd leak when transferring empty files
  with dnd
- add support for passing a username with SASL authentication
- hide guest cursor when ungrabbing mouse in server mode
- make sure client cursor is in the same position as the guest cursor when
  ungrabbing mouse in server mode
- add man page for command line options of application using spice-gtk
- strip '\0' from text clipboard data
- fix synchronization of keyboard modifiers
- coroutine improvements
- use http by default when SPICE_PROXY uri has no scheme

v0.25
=====

- Fix SPICE_GTK_MICRO_VERSION define for default value
- Make "phodav", the webdav server, an external dependency rather than
  a submodule

v0.24
=====

- support folder sharing, via WebDAV channel
- add HTTPS proxy support (requires glib 2.28), and Basic auth
- add SPICE_GTK_CHECK_VERSION macro
- advertise SASL capability early (to help fips-enabled servers)
- fix crash when releasing primary surface
- fix a few memory leaks with SASL
- fix spice_display_get_pixbuf() with offset area
- build-sys improvements
- note: until now, providing an invalid plain-port didn't error, and
  was falling back silently on tls-port. With this release, an error
  will be reported if the port can't be opened.

v0.23
=====

- support Opus codec for audio channels
- ssl: use tls 1.0 or better
- support gdbus instead of dbus-glib when available
- misc build-sys, compile and runtime fixes

v0.22
=====

- improve inverted cursor support
- use system-wide trust certificate store
- make sasl support work with other method than MD5
- fix some clipboard crasher, limit clipboard size
- fix various regressions:
  usbredir, alt-tab on win32, palette crash, agent notification, old
  protocol support, sasl ending crash, gthread coroutine crash, close
  sockets on migration, pulse backend crash
- fix a few memory leaks
- build-sys improvements

v0.21
=====

- improve inverted cursor support
- win32 usb redirected device uninstall fix
- add support for libusb hotplug API
- smartcard initialization fixes
- c&p converts line-endings if necessary
- rendering and overall performance improvements
- build and bindings fixes

v0.20
=====

- adaptive video streaming support (sync with PulseAudio backend only)
- add spice_usb_device_manager_get_devices_with_filter()
- add --spice-secure-channels to explicitely specify secure channels
- multi-monitor, win32, USB redir fixes
- add basic gtk+ wayland and broadway backend support
- removed the GnomeRR code

v0.19
=====

This is a bugfix only release, except the snappy name change
- snappy has been renamed to spicy-screenshot
- Several file-xfer fixes and improvements
- Many win32 and USB redirection related fixes
- Compile and work again with RHEL6 and older glib releases
- misc fixes and improvements

v0.18
=====

- Build fix with Gtk+ unstable.
- MinGW build fixes with old headers
- Fix USB coldplug race
- Fixes rhbz#908057

v0.17
=====

- Update spice-common with fedora 875348, 826036 fixes
- Multi-monitor fixes (avoid monitor order shuffling, fix mouse offset
  if monitor 0 is not at +0+0 and let agent do monitor offset)
- Add support for VD_AGENT_CAP_SPARSE_MONITORS_CONFIG
- Add controller & session "proxy" properties
- Add drag and drop file copy support to send file to guest, you will
  need capable agent to use that feature. Adds spice_main_file_copy_async()
- Introspection fixes
- Build fixes

v0.16
=====

- Fix crash with SSL connection (#890464)
- Send monitor config to the agent on spice_main_set_display_enabled() (#881072)
- Fix channel leak and wrong condition in spice_channel_flush()
- Build fixes

v0.15
=====

- Add HTTP Proxy support (only with glib >= 2.26)
- Add "port" channel support, to allow arbitrary communication on top
  of spice connection
- usb-redir: fix migration support
- win32: various keyboard & mouse fixes
- Add info message when USB dialog is empty
- Fix initial black screen on some 16bits guest
- Various bug fixes and improvements

v0.14
=====

- Support for seamless migration
- Improve scaling handling, add downscale-only property to give more
  control over scaling
- Better handle key press/release events in high-latency situations,
  this should avoid unwanted key repetitions
- Improve unescaping in URI parsing
- Fix symbol versioning which was broken in 0.13
- Fix for CVE-2012-4425
- Various bug fixes and improvements

v0.13
=====

- ABI break! SONAME has been bumped, all programs and libraries
  linking to spice-gtk need to be recompiled against this version
- Add support for USB device redirection on Windows
- Add monitors config support (multiple monitors in same display)
- Inhibit automount on GNOME desktop, to ease USB redirection
- Better video support (reduce some glitches)
- Misc migration fixes
- Various bug fixes and improvements

v0.12
=====

- Fix memory leak when guest is resized
- Fix color-depth setting
- Hide/Show cursor correctly when needed
- Fix blue-tinted video with old Spice servers
- Correct scroll-event not received with recent Gtk+
- Fix various migrations issues
- Allow to disable CELT encoding at runtime with SPICE_DISABLE_CELT
- Various crash fixes (on pubkey, recording, clipboard)
- Build changes (common submodule) and fixes

v0.11
=====

- Fix semi-seamless migration regression
- Add Spice session UUID and name support
- Add foreign menu support to controller library
- Add a simple controller testing tool spice-controller-dump
- Build fixes

v0.10
=====

- USB redir is now aware of host/guest side filtering
- you can query spice_usb_device_manager_can_redirect_device()
- fix the usbredir channel lifetime to be equal to session lifetime
- set keepalive on channel socket
- fix hangs on windows when using ssl chanels
- add a SpiceDisplay::zoom-level to maintain a scaling ratio
- add controller ENABLE_SMARTCARD option
- remove a few warnings, ui improvements, build fixes

v0.9
====

- Add command line options for setting the cache size and the glz window size
- Add a USB device selection widget to libspice-client-gtk
- Various bug fixes and code improvements

v0.8
====

- add USB redirection support, see Hans comments in the log and that
  post for details: http://hansdegoede.livejournal.com/11084.html
- introduce SpiceGtkSession to deal with session-wide Gtk events, such
  as clipboard, instead of doing it per display
- many cursor and keyboard handling improvements
- handle the new "semi-seamless" migration
- support new Spice mini-headers
- better coroutines: fibers on windows & jmp on linux
- add Vala vapi bindings generation
- many bug fixes and code improvements

v0.7
====

- smartcard support
- better video playback performance (jpeg-turbo & audio improvements)
- support for audio volume (needs qemu support)
- controller support for Windows (NamedPipe)
- make perl-Text-CSV optional for tarball builds
- new spice_get_option_group()/spice_set_session_option()
- keyboard improvements, grab-sequence can be configured, various windows fixes
- new tool spicy-stats, to collect informations during a session
- bugfixes: memleak fixes, SASL fixes, crash with virt-manager
- various build fixes, should build on MacOS as well now

v0.6
====

- multi-head is working now!
- change client resolution if guest can't
- support sharing large clipboard, and images
- multiple clibpoard selection
- support SASL authentication
- add experimental/unstable controller API
- and a bunch of various smaller fixes

v0.5
====

- Compatibility with gtk2 and gtk3
- Migrations: seamless and switch host methods
- SSL verification: public key, subject and host checks added
- spice:// url parsing learned "password" argument
- spicy: recent connexions UI added
- various minor fixes

v0.4
====

- sync video with pulseaudio backend
- build with mingw, and run on Windows
- various minor fixes

v0.3
====

- fix Windows QXL driver support
- fully asynchronous operations using coroutines
  (thanks go to gtk-vnc devs)
- cairo display (old XShm display can be enabled with --with-x11)
- scaling support for cairo display
- experimental audio support using GStreamer
- API reference gtk-doc
- more cursor type support
- various fixes and cleanup

v0.2
====

- gtk: disconnect record stream when record_stop()
- README: add a few missing dependencies
- build: use git-version-gen
- build: re-enable -Wflags, and fix a few warnings
- build: fix make -j
- gtk: add zlib decoder
- gtk: add jpeg decoder
- gtk: progressive agent message recomposition
- gtk: add dispay config
- gtk: add clipboard sharing for text
- TODO: update
- gtk: put some g_message() under SPICE_DEBUG
- gtk: add channel.set_capability()
- gtk: add {session,channel}_open_fd()
- gtk: add CELT playback
- gtk: add CELT recording
- gtk: save/restore spicy configuration
- gtk: don't uncork new streams
- gtk: delay PA stream creation when context is ready
- gtk: visibility option for statusbar/toolbar in spicy

v0.1.0
======

- desktop display, using GLZ compression
- audio playback/recording with PulseAudio
- video in mjpeg
- python and gobject-introspection modules
- spicy: a simple Gtk client
- snappy: a command line screenshot tool
