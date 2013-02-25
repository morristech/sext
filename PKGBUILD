pkgname=sext
pkgver=0.$(date +%s)
pkgrel=1
ver_sm=2.16 #seamonkey
ver_go=19.0 #gecko
ver_ff=19.0 #firefox
pkgdesc="Altered seamonkey extensions"
arch=(any)
license=('GPL')
makedepends=(wget xmlstarlet proterozoic zip unzip sqlite3)
depends=(seamonkey=$ver_sm)
install=install
pastvers=(2.5 2.6 2.6.1 2.7 2.7.1 2.7.2 2.8 2.9 2.10 2.11 2.12.1 2.13 2.13.1 2.13.2 2.14 2.14.1 2.15.1 2.15.2)
source=("https://static.addons.mozilla.net/_files/309/littlemonkey_for_seamonkey-1.8.76-sm.xpi"
		  "http://downloads.mozdev.org/xsidebar/mods/abduction_screen_capture-3.0.14-mod.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/1865/adblock_plus-2.2.3-tb+an+sm+fx.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/6623/betterprivacy-1.68-fx.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/4550/compact_menu_2-4.3.1-fx+sb+sm+tb-linux.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/311084/cookiesafe_ff_4_compatible-3.1a5-sm+tb+fx.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/3255/cookieswap-0.5.284-fx.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/336172/copy_pure_text-2.0.1-sm+fx+tb.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/156490/duplicate_this_tab-1.3-fx+sm.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/220/flashgot-1.5.4.2-fx+tb+sm.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/2464/foxyproxy_standard-4.1.3-fx+sm+tb.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/337195/google_privacy-0.2.3-sm+fx.xpi"
		  "https://www.eff.org/files/https-everywhere-4.0development.5.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/722/noscript-2.6.5.7-sm+fx+fn.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/1759/organize_status_bar-0.6.4-fx.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/953/refcontrol-0.8.16-sm+fx.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/9727/requestpolicy-0.5.27-fx+sm.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/8016/show_my_password-2.0-fx+sm.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/3173/trackmenot-0.6.728-fx+sm.xpi"
		  "https://addons.cdn.mozilla.net/storage/public-staging/59/user_agent_switcher-0.7.3-fx+sm.xpi")
noextract=("${source[@]##*/}")
md5sums=("e4280b110334b67fcfc9567100ef7e5b"	# littlemonkey
			"969fb1037482120a1d81ae0253e36319"	# abduction
			"07607a3cb349eeccfc7768b5f4f2aaae"	# adblock plus
			"efac8cd8fe05bf0a7d173f92e481e65a"	# betterprivacy
			"269401fde20879ec4f869052a7c8a37d"	# compact menu
			"5b99c2c66a39e358aa64ae368a67d475"	# cookiesafe
			"3bdc81f16f06a70968ec41792f4dd93e"	# cookieswap
			"29ff52ebd23ed5ab8e331a808dee9062"	# copy pure text
			"83a4c672016723021e38ed4925dd491f"	# duplicate this
			"0282708ba3f7623ff91f105adc9bfd74"	# flashgot
			"1e648de48b6f4323a3eaade28486b3c2"	# foxyproxy
			"f441d80dacc34d33f8b7d369c9191ec8"	# google privacy
			"42be9f24595a4bcd792350799b687bb9"	# https everywhere
			"82816e7d024c71d698dd108c0aec527d"	# noscript
			"d8a91a585a2cf2a0e073c90e4b72f7c4"	# organize status bar
			"72911f3df8cb79b9cfbce5a36296e03d"	# refcontrol
			"f772e5c1ac31706a3211d0d4bab190a3"	# requestpolicy
			"5aa14241662f9b1ac446cf1f80e71047"	# show my password
			"533d19c08df11939dbaa7f7952238ccf"	# track me not
			"d7f1f4b3689bf61c3d583432872a4cc2")	# user agent switcher
# last checked for updates: Feb 24 2013
# fireshot
# proxy tool
# beefree <-- breaks statusbar!
build() {
	 sed -i \
		  -e "s/^\(ver_sm=\).*$/\1$ver_sm/" \
		  -e "s/^\(pastvers=\).*$/\1(${pastvers[*]})/" $startdir/install
}
package() {
	 local smdir=$pkgdir/usr/lib/seamonkey-$ver_sm ffdir=$pkgdir/usr/lib/firefox
	 local smprof=$smdir/defaults/profile ffprof=$ffdir/defaults/profile
	 local xpi section
	 mkdir -p $smdir/extensions $ffdir/extensions $ffdir/defaults/profile
	 for xpi in $srcdir/*.xpi; do
		  echo "Fixing $(basename "$xpi") ..."
		  fix-extension $xpi $smdir/extensions
	 done
	 install -D {$smdir,$ffdir}/extensions/{57068FBE-1506-42ee-AB02-BD183E7999E4}.xpi
	 rm -f $smdir/extensions/https-everywhere@eff.org/chrome/content/rules/GoogleMaps.xml~HEAD
	 install -D {$srcdir/..,$smprof/useragentswitcher}/useragents.xml
	 install -D {$srcdir/..,$smprof/adblockplus}/patterns.ini
	 install -D {$srcdir/..,$smprof}/localstore.rdf.sxt
	 install -D {$srcdir/..,$smprof}/foxyproxy.xml
	 install -D {$srcdir/..,$smprof}/cert_override.txt
	 install -D {$srcdir/..,$ffprof}/cert_override.txt
	 install -D {$srcdir/..,$smdir/defaults/pref}/local-settings.js
	 install -D {$srcdir/..,$ffdir/defaults/pref}/local-settings.js
	 install -D {$srcdir/..,$smdir}/mozilla.cfg
	 install -D $srcdir/../mozilla.ff.cfg $ffdir/mozilla.cfg
	 install -D $srcdir/../localstore.ff.rdf $ffdir/defaults/profile/localstore.rdf
	 sed -i \
		  -e s/%VER_SM%/$ver_sm/ig \
		  -e s/%VER_FF%/$ver_ff/ig \
		  -e s/%VER_GO%/$ver_go/ig {$smdir,$ffdir}/mozilla.cfg

	 rps_section() { grep -Pzo '(?<=\['"${1}"'\]\n)[^[]*' $srcdir/../site-rules.txt; }
	 section_to_pref()  { echo        'pref("'"$2"'","'$(rps_section "$1")'");' >> $smdir/mozilla.cfg; }
	 section_to_dpref() { echo 'defaultPref("'"$2"'","'$(rps_section "$1")'");' >> $smdir/mozilla.cfg; }
	 section_to_pref	origins						extensions.requestpolicy.allowedOrigins
	 section_to_pref	destinations				extensions.requestpolicy.allowedDestinations
	 section_to_pref	origins-to-destinations	extensions.requestpolicy.allowedOriginsToDestinations
	 section_to_dpref	noscript-untrusted		noscript.untrusted
	 section_to_dpref	noscript-sites				capability.policy.maonoscript.sites

	 for section in origins destinations origins-to-destinations; do
		  echo "[$section]" >> $smdir/requestpolicy-rules.txt
		  rps_section "$section" >> $smdir/requestpolicy-rules.txt
	 done
	 sed -i '/^$/d' $smdir/requestpolicy-rules.txt # deletes empty lines

	 to_cookietype() {
		  while read; do
				echo "INSERT INTO \"moz_hosts\" VALUES(NULL,'${REPLY}','cookie',${1},0,0);"
		  done
	 }; {
		  cat $srcdir/../permissions.sqlite.dump
		  rps_section cookies-temp | to_cookietype 8
		  rps_section cookies-full | to_cookietype 1
		  echo "COMMIT;"
	 } | sqlite3 $smprof/permissions.sqlite

	 # awful hack until fix-extension can deal with commented-out fields!
	 betterprivacy="$smdir/extensions/{d40f5e7b-d2cf-4856-b441-cc613eeffbe3}.xpi"
	 tmpfile=/tmp/.bp.$(date +%s)
	 unzip -qp "$betterprivacy" install.rdf >| $tmpfile
	 sed 's/<!--\(em:targetApplication.*\)-->/<\1>/' $tmpfile \
		  | rezip "$betterprivacy" install.rdf
	 rm -f "$tmpfile"
}
