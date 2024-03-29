ignore_headers = [
  'bio-gio.h',
  'channel-display-priv.h',
  'channel-usbredir-priv.h',
  'client_sw_canvas.h',
  'continuation.h',
  'coroutine.h',
  'decode.h',
  'desktop-integration.h',
  'gio-coroutine.h',
  'giopipe.h',
  'smartcard-manager-priv.h',
  'spice-audio-priv.h',
  'spice-channel-cache.h',
  'spice-channel-priv.h',
  'spice-common.h',
  'spice-file-transfer-task-priv.h',
  'spice-grabsequence-priv.h',
  'spice-gstaudio.h',
  'spice-gtk-session-priv.h',
  'spice-marshal.h',
  'spice-session-priv.h',
  'spice-uri-priv.h',
  'spice-util-priv.h',
  'spice-widget-priv.h',
  'usb-acl-helper.h',
  'usb-device-manager-priv.h',
  'usbdk_api.h',
  'usbutil.h',
  'vmcstream.h',
  'vncdisplaykeymap.h',
  'win-usb-dev.h',
]

spice_gtk_doc_dep = declare_dependency(link_with : [spice_client_gtk_lib, spice_client_glib_lib])

glib_prefix = dependency('glib-2.0').get_variable(pkgconfig: 'prefix')
glib_docpath = glib_prefix / 'share' / 'gtk-doc' / 'html'
gtk_prefix = dependency('gtk+-3.0').get_variable(pkgconfig: 'prefix')
gtk_docpath = gtk_prefix / 'share' / 'gtk-doc' / 'html'
docpath = spice_gtk_datadir / 'gtk-doc' / 'html'

gnome.gtkdoc(meson.project_name(),
             dependencies : spice_gtk_doc_dep,
             main_xml : meson.project_name() + '-docs.xml',
             ignore_headers : ignore_headers,
             include_directories: spice_gtk_include,
             c_args : '-DSPICE_COMPILATION',
             install : true,
             scan_args : [
               '--deprecated-guards="SPICE_DISABLE_DEPRECATED"',
               '--ignore-decorators="G_GNUC_INTERNAL"',
               '--rebuild-types',
               meson.project_build_root() / 'src' / 'spice-version.h'
             ],
             src_dir : meson.project_source_root() / 'src',
             fixxref_args: [
               '--html-dir=@0@'.format(docpath),
               '--extra-dir=@0@'.format(glib_docpath / 'glib'),
               '--extra-dir=@0@'.format(glib_docpath / 'gobject'),
               '--extra-dir=@0@'.format(glib_docpath / 'gio'),
               '--extra-dir=@0@'.format(gtk_docpath / 'gtk3'),
             ],
            )
