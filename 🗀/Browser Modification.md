Even though I don't use Chromium-based browsers, here's some sources I find informative:
- https://youtu.be/V5cdFJqknE8
- https://youtu.be/wMe3SPBJ6iQ?t=119
- https://youtu.be/9nl6hO0ECgM?t=515
- https://thewindowsclub.com/google-chrome-flag-settings-windows
- https://reddit.com/r/browsers/comments/107cj5b/what_are_your_top_chromeflags_or_braveflags

I use Floorp & Zen Browser, both of which focus heavily on privacy & security and already have most preference settings configured by default, so I might not reference all of them here. Instead, refer to these sources:
- https://reddit.com/r/firefox/comments/17hlkhp/what_are_your_must_have_changes_in_aboutconfig
- https://reddit.com/r/firefox/comments/1ezjps2/what_settings_you_use_on_aboutconfig
- https://github.com/SpitFire-666/Firefox-Stuff?tab=readme-ov-file#-recommended-settings


```
media.peerconnection.enabled = false
privacy.resistFingerprinting = true
privacy.trackingprotection.fingerprinting.enabled = true
privacy.trackingprotection.enabled = true
geo.enabled = false
media.navigator.enabled = false
network.dns.disablePrefetch = true
network.prefetch-next = false
webgl.disabled = true
dom.event.clipboardevents.enabled = false
browser.urlbar.trimURLs = false
layout.spellcheckDefault = 2
security.ssl.require_safe_negotiation = true
security.tls.enable_0rtt_data = false
security.ssl.enable_false_start = false
browser.tabs.cardPreview.enabled = true [as of writing this both floorp and zen browser have this enabled by default but doesn't work]
browser.newtabpage.activity-stream.feeds.telemetry = false
browser.newtabpage.activity-stream.telemetry = false
browser.search.region = US [set country code to your preference]
devtools.f12_enabled = false [false if not using dev tools]
accessibility.force_disabled = 1 [support.mozilla.org/kb/accessibility-features-firefox]
network.captive-portal-service.enabled = false [when free wifi redirects to their shitty site]
network.notify.checkForProxies = false
browser.tabs.unloadOnLowMemory = true
media.hardware-video-decoding.force-enabled = true
media.ffmpeg.vaapi.enabled = true
network.ssl_tokens_cache_capacity = 32768
network.predictor.enable-hover-on-ssl = true
network.predictor.enable-prefetch = true
network.predictor.preconnect-min-confidence = 20
network.predictor.prefetch-force-valid-for = 3600
network.predictor.prefetch-min-confidence = 30
network.predictor.prefetch-rolling-load-count = 120
network.predictor.preresolve-min-confidence = 10
layers.acceleration.force-enabled = true [if you have a compatible GPU with latest drivers and you’re experiencing rendering or performance issues]
```
