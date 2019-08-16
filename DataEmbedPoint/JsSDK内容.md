```javascript
!function (e) {
	function t(r) {
		if (n[r]) return n[r].exports;
		var i = n[r] = {i: r, l: !1, exports: {}};
		return e[r].call(i.exports, i, i.exports, t), i.l = !0, i.exports
	}

	var n = {};
	t.m = e, t.c = n, t.i = function (e) {
		return e
	}, t.d = function (e, n, r) {
		t.o(e, n) || Object.defineProperty(e, n, {configurable: !1, enumerable: !0, get: r})
	}, t.n = function (e) {
		var n = e && e.__esModule ? function () {
			return e.default
		} : function () {
			return e
		};
		return t.d(n, "a", n), n
	}, t.o = function (e, t) {
		return Object.prototype.hasOwnProperty.call(e, t)
	}, t.p = "", t(t.s = 26)
}([function (e, t, n) {
	"use strict";
	e.exports = function () {
		var e = arguments[0];
		if (arguments.length > 1) for (var t = 1; t < arguments.length; t++) for (var n in arguments[t]) e[n] = arguments[t][n];
		return e
	}
}, function (e, t, n) {
	"use strict";
	"user strict";
	var r = n(9), i = n(5), o = void 0, a = window.LS, s = "analytics_user_id_" + i.version,
		u = "analytics_anonymous_id_" + i.version;
	e.exports = {
		getId: function () {
			if (o) return o.message_id = r(), o;
			var e = a.get(s), t = a.get(u);
			return t || (t = r(), a.set(u, t)), o = {}, o.anonymous_id = t, o.user_id = e || "", o.message_id = r(), o
		}, setUserId: function (e) {
			a.set(s, e), o && (o.user_id = e)
		}, delUserId: function () {
			a.remove(s), o && delete o.user_id
		}
	}
}, function (e, t, n) {
	"use strict";
	n(17);
	var r = n(0), i = n(12);
	window.analytics = function (e) {
		return e = r({postUrl: "https://api.yzztech.com/api/v1", apiKey: "", context: {}, autoPV: !0}, e), i(e)
	}, e.exports = window.analytics
}, function (e, t, n) {
	"use strict";
	var r = n(5), i = n(6), o = window.document, a = window.location, s = window.screen;
	e.exports = {
		page: {path: a.pathname, referrer: o.referrer, host: a.hostname, title: o.title},
		user_agent: window.navigator.userAgent,
		library: {name: r.name, version: r.version},
		screen: {width: s.width, height: s.height, density: window.devicePixelRatio || 1},
		campaign: i.getValue()
	}
}, function (e, t, n) {
	"use strict";
	var r = n(23);
	e.exports = function (e) {
		var t = {
			url: "", success: function () {
			}, error: function () {
			}, type: "GET", data: null, async: !0, apiKey: ""
		};
		for (var n in e) t[n] = e[n];
		var i = "get" === t.type.toLowerCase();
		if (i && t.data && (t.url += "?" + r.stringify(t.data), delete t.data), "XDomainRequest" in window && window.XDomainRequest) {
			var o = new XDomainRequest;
			return o.open(t.type, t.url), o.onload = function () {
				t.success(o.responseText, o)
			}, o.onerror = function () {
				t.error && t.error(o)
			}, void (i ? o.send() : o.send(t.data ? JSON.stringify(t.data) : ""))
		}
		var a = new XMLHttpRequest;
		a.open(t.type.toUpperCase(), t.url, t.async), i || null === t.data || a.setRequestHeader("Content-Type", "application/json;charset=UTF-8"), a.setRequestHeader("X-API-KEY", t.apiKey), i ? a.send() : a.send(t.data ? JSON.stringify(t.data) : ""), a.onreadystatechange = function () {
			4 == parseInt(a.readyState, 10) && (200 == parseInt(a.status, 10) ? t.success(a.responseText, a) : t.error && t.error(a))
		}
	}
}, function (e, t, n) {
	"use strict";
	e.exports = {name: "analytics-js", version: "1.0.0"}
}, function (e, t, n) {
	"use strict";
	"user strict";

	function r(e, t) {
		if (!(e instanceof t)) throw new TypeError("Cannot call a class as a function")
	}

	var i = function () {
		function e(e, t) {
			for (var n = 0; n < t.length; n++) {
				var r = t[n];
				r.enumerable = r.enumerable || !1, r.configurable = !0, "value" in r && (r.writable = !0), Object.defineProperty(e, r.key, r)
			}
		}

		return function (t, n, r) {
			return n && e(t.prototype, n), r && e(t, r), t
		}
	}(), o = n(16), a = n(18), s = window.LS, u = "campaign", c = {
		utm_source: "source",
		utm_medium: "medium",
		utm_campaign: "campaign",
		utm_term: "term",
		utm_content: "content"
	}, l = function () {
		var e = {};
		for (var t in c) {
			var n = a.get(t);
			n && (e[c[t]] = n)
		}
		return e
	}, d = function () {
		function e() {
			r(this, e), this.init()
		}

		return i(e, [{
			key: "init", value: function () {
				var e = l();
				e.source && this.setValue(e)
			}
		}, {
			key: "getValue", value: function () {
				var e = s.get(u);
				try {
					e = JSON.parse(e)
				} catch (t) {
					e = {}
				}
				return e
			}
		}, {
			key: "setValue", value: function (e) {
				return o.isPlainObject(e) && s.set(u, JSON.stringify(e)), this
			}
		}, {
			key: "clear", value: function () {
				return s.remove(u), this
			}
		}]), e
	}();
	e.exports = new d
}, function (e, t) {
	function n(e, t) {
		var n = t || 0, i = r;
		return i[e[n++]] + i[e[n++]] + i[e[n++]] + i[e[n++]] + "-" + i[e[n++]] + i[e[n++]] + "-" + i[e[n++]] + i[e[n++]] + "-" + i[e[n++]] + i[e[n++]] + "-" + i[e[n++]] + i[e[n++]] + i[e[n++]] + i[e[n++]] + i[e[n++]] + i[e[n++]]
	}

	for (var r = [], i = 0; i < 256; ++i) r[i] = (i + 256).toString(16).substr(1);
	e.exports = n
}, function (e, t) {
	var n = "undefined" != typeof crypto && crypto.getRandomValues.bind(crypto) || "undefined" != typeof msCrypto && msCrypto.getRandomValues.bind(msCrypto);
	if (n) {
		var r = new Uint8Array(16);
		e.exports = function () {
			return n(r), r
		}
	} else {
		var i = new Array(16);
		e.exports = function () {
			for (var e, t = 0; t < 16; t++) 0 == (3 & t) && (e = 4294967296 * Math.random()), i[t] = e >>> ((3 & t) << 3) & 255;
			return i
		}
	}
}, function (e, t, n) {
	function r(e, t, n) {
		var r = t && n || 0;
		"string" == typeof e && (t = "binary" === e ? new Array(16) : null, e = null), e = e || {};
		var a = e.random || (e.rng || i)();
		if (a[6] = 15 & a[6] | 64, a[8] = 63 & a[8] | 128, t) for (var s = 0; s < 16; ++s) t[r + s] = a[s];
		return t || o(a)
	}

	var i = n(8), o = n(7);
	e.exports = r
}, function (e, t, n) {
	"use strict";
	var r = n(1);
	e.exports = {
		logout: function () {
			return r.delUserId()
		}, getAnonymousId: function () {
			return r.getId().anonymous_id
		}, getUserId: function () {
			return r.getId().user_id
		}
	}
}, function (e, t, n) {
	"use strict";
	var r = n(4), i = n(1), o = n(0), a = n(3);
	e.exports = function (e) {
		return function (t, n, s) {
			if (i.setUserId(t), !n) return !1;
			var u = o({properties: n, type: "identify", context: o(a, e.context)}, i.getId());
			r({
				url: e.postUrl + "/identify", data: u, type: "post", apiKey: e.apiKey, done: function (e, t) {
					s && s(null, e, t)
				}, error: function (e) {
					s && s(e)
				}
			})
		}
	}
}, function (e, t, n) {
	"use strict";
	var r = n(15), i = n(11), o = n(14), a = n(10), s = n(20), u = n(0), c = n(6), l = n(24), d = n(19);
	e.exports = function (e) {
		var t = e.autoPV, n = {
			track: r(e),
			identify: i(e),
			model: o(e),
			video: s(e),
			getAnonymousId: a.getAnonymousId,
			getUserId: a.getUserId,
			logout: a.logout,
			campaign: c,
			utils: {extend: u, uuid: l}
		};
		if (t && !d.isSpider()) {
			var p = performance.timing.requestStart;
			window.addEventListener("load", function () {
				var e = performance.timing.domContentLoadedEventEnd;
				n.track("page.view", {loaded_time: e - p})
			}, !1)
		}
		return n
	}
}, function (e, t, n) {
	"use strict";
	var r = function (e, t, n, r) {
		this.sdk = e, this.player = t, this.res = this.player.querySelectorAll("source"), this.config = this.initConfig(n), this.playerCount = 0, this.playingEvent = !1, this.callback = r, this.current = [], this.eventList = {}, this.init()
	};
	r.prototype = {
		video: {
			loaded: function () {
				this.track("video.loaded", {})
			}, played: function (e) {
				this.playing(), this.track("video.played", {is_first_play: e})
			}, paused: function () {
				this.stopPlaying(), clearInterval(this.playing), this.track("video.paused", {})
			}, stoped: function () {
				this.stopPlaying(), this.track("video.stoped", {})
			}, seeked: function (e, t) {
				this.track("video.seeked", {position: e, to_position: t})
			}, playing: function () {
				this.track("video.playing", {})
			}, interrupted: function (e) {
				this.stopPlaying(), this.track("video.interrupted", {method: e})
			}
		}, init: function () {
			this.ready(), this.timeupdate(), this.start(), this.volumechange(), this.stop(), this.seeked(), this.pause(), this.fullscreen(), this.playerror(), this.leave(), this.destroy(), this.setup()
		}, status: {ready: !1, stop: !1, pause: !1, play: !1}, track: function (e, t) {
			var n = this.sdk;
			t = this.sdk.utils.extend({}, this.config, {position: this.player.currentTime}, t), n.track(e, t, this.callback)
		}, initConfig: function (e) {
			var t = {session_id: this.sdk.utils.uuid.v4(), video_length: 0, position: 0, is_fullscreen: !1};
			return this.sdk.utils.extend({}, t, e)
		}, ready: function () {
			var e = this, t = function () {
				e.config.video_id = e.config.video_id || e.player.currentSrc, e.config.sound = 100 * e.player.volume, e.config.video_length = e.player.duration, e.player.muted && (e.config.sound = 0), e.current = [e.player.currentTime, e.player.currentTime], e.video.loaded.call(e)
			};
			this.eventList.loadeddata = {dom: this.player, event: t}
		}, timeupdate: function () {
			var e = this, t = function (t) {
				e.current.push(e.player.currentTime), e.current.shift()
			};
			this.eventList.timeupdate = {dom: this.player, event: t}
		}, start: function () {
			var e = this, t = function (t) {
				e.player.seeking || (e.playerCount++, e.video.played.call(e, 1 === e.playerCount))
			};
			this.eventList.play = {dom: this.player, event: t}
		}, volumechange: function () {
			var e = this, t = function (t) {
				e.config.sound = 100 * e.player.volume, e.player.muted && (e.config.sound = 0)
			};
			this.eventList.volumechange = {dom: this.player, event: t}
		}, stop: function () {
			var e = this, t = function (t) {
				e.video.stoped.call(e)
			};
			this.eventList.ended = {dom: this.player, event: t}
		}, seeked: function () {
			var e = this, t = function (t) {
				e.seeking = {play: [e.current[0], e.current[1]], stop: [e.current[1], e.player.currentTime]}
			}, n = function (t) {
				var n = e.player.paused ? e.seeking.stop : e.seeking.play;
				e.video.seeked.call(e, n[0], n[1])
			};
			this.eventList.seeking = {dom: this.player, event: t}, this.eventList.seeked = {dom: this.player, event: n}
		}, pause: function () {
			var e = this, t = function (t) {
				e.player.seeking || e.player.ended || e.video.paused.call(e)
			};
			this.eventList.pause = {dom: this.player, event: t}
		}, fullscreen: function () {
			var e = this, t = function (t) {
				e.config.is_fullscreen = document[e.prefix + "IsFullScreen"]
			};
			this.eventList[this.prefix + "fullscreenchange"] = {dom: document, event: t}
		}, playing: function () {
			var e = this;
			this.playingEvent = setInterval(function () {
				e.video.playing.call(e)
			}, 1e4)
		}, stopPlaying: function () {
			clearInterval(this.playingEvent)
		}, playerror: function () {
			var e = this, t = this.player.src ? this.player : this.res.length ? this.res[this.res.length - 1] : null,
				n = function (t) {
					e.video.interrupted.call(e, "瑙嗛璧勬簮涓嶅彲鐢�")
				}, r = function (t) {
					e.video.interrupted.call(e, "瑙嗛璧勬簮涓虹┖")
				};
			t && (this.eventList.error = {dom: t, event: n}), this.eventList.emptied = {dom: this.player, event: r}
		}, leave: function () {
			var e = this, t = function (t) {
				e.config.position = e.player.currentTime, e.video.interrupted.call(e, "绂诲紑椤甸潰")
			};
			this.eventList.unload = {dom: window, event: t}
		}, setup: function () {
			for (var e in this.eventList) {
				var t = this.eventList[e];
				t.dom.addEventListener(e, t.event, !1)
			}
		}, destroy: function () {
			this.stopPlaying();
			for (var e in this.eventList) {
				var t = this.eventList[e];
				t.dom.removeEventListener(e, t.event, !1)
			}
		}, prefix: function () {
			var e = window.getComputedStyle(document.documentElement, "");
			return (Array.prototype.slice.call(e).join("").match(/-(moz|webkit|ms)-/) || "" === e.OLink && ["", "o"])[1]
		}()
	}, e.exports = r
}, function (e, t, n) {
	"use strict";
	var r = n(4), i = n(1), o = n(0), a = n(3);
	e.exports = function (e) {
		return function (t, n, s) {
			var u = o({properties: n, model: t, type: "model", context: o(a, e.context)}, i.getId());
			r({
				url: e.postUrl + "/model", data: u, type: "post", apiKey: e.apiKey, done: function (e, t) {
					s && s(null, e, t)
				}, error: function (e) {
					s && s(e)
				}
			})
		}
	}
}, function (e, t, n) {
	"use strict";
	var r = n(4), i = n(1), o = n(0), a = n(3);
	e.exports = function (e) {
		return function (t, n, s) {
			var u = o({properties: n, event: t, type: "track", context: o(a, e.context)}, i.getId());
			r({
				url: e.postUrl + "/track", data: u, type: "post", apiKey: e.apiKey, done: function (e, t) {
					s && s(null, e, t)
				}, error: function (e) {
					s && s(e)
				}
			})
		}
	}
}, function (e, t, n) {
	"use strict";
	e.exports = {
		getTypeof: function (e) {
			return Object.prototype.toString.call(e)
		}, isPlainObject: function (e) {
			return "[object Object]" === this.getTypeof(e)
		}
	}
}, function (e, t, n) {
	"use strict";
	!function (e) {
		var t, n = function () {
		}, r = e.document, i = {set: n, get: n, remove: n, clear: n, each: n, obj: n, length: 0};
		!function () {
			if ("localStorage" in e) try {
				return void (t = e.localStorage)
			} catch (e) {
			}
			var n, i, o = r.getElementsByTagName("head")[0], a = e.location.hostname || "localStorage", s = new Date;
			if (o.addBehavior) {
				try {
					i = new ActiveXObject("htmlfile"), i.open(), i.write('<script>document.w=window;<\/script><iframe src="/favicon.ico"></iframe>'), i.close(), n = i.w.frames[0].document, o = n.createElement("head"), n.appendChild(o)
				} catch (e) {
					o = r.getElementsByTagName("head")[0]
				}
				try {
					s.setDate(s.getDate() + 36500), o.addBehavior("#default#userData"), o.expires = s.toUTCString(), o.load(a), o.save(a)
				} catch (e) {
					return
				}
				var u, c;
				try {
					u = o.XMLDocument.documentElement, c = u.attributes
				} catch (e) {
					return
				}
				var l = new RegExp("^p__hack_"), d = new RegExp("m-_-c", "g"), p = function (e) {
					return encodeURIComponent("p__hack_" + e).replace(/%/g, "m-_-c")
				}, f = function (e) {
					return decodeURIComponent(e.replace(d, "%")).replace(l, "")
				};
				t = {
					length: c.length, isVirtualObject: !0, getItem: function (e) {
						return (c.getNamedItem(p(e)) || {nodeValue: null}).nodeValue || u.getAttribute(p(e))
					}, setItem: function (e, t) {
						try {
							u.setAttribute(p(e), t), o.save(a), this.length = c.length
						} catch (e) {
						}
					}, removeItem: function (e) {
						try {
							u.removeAttribute(p(e)), o.save(a), this.length = c.length
						} catch (e) {
						}
					}, clear: function () {
						for (; c.length;) this.removeItem(c[0].nodeName);
						this.length = 0
					}, key: function (e) {
						return c[e] ? f(c[e].nodeName) : void 0
					}
				}, "localStorage" in e || (e.localStorage = t)
			} else try {
				t = e.localStorage
			} catch (e) {
				t = null
			}
		}(), e.LS = t ? {
			set: function (e, n) {
				void 0 !== this.get(e) && this.remove(e), t.setItem(e, n), this.length = t.length
			}, get: function (e) {
				var n = t.getItem(e);
				return null === n ? void 0 : n
			}, remove: function (e) {
				t.removeItem(e), this.length = t.length
			}, clear: function () {
				t.clear(), this.length = 0
			}, each: function (e) {
				var t, n = this.obj(), r = e || function () {
				};
				for (t in n) if (!1 === r.call(this, t, this.get(t))) break
			}, obj: function () {
				var e, n, r = {}, i = 0;
				if (t.isVirtualObject) r = t.key(-1); else for (e = t.length; i < e; i++) n = t.key(i), r[n] = this.get(n);
				return r
			}, length: t.length
		} : i, e.jQuery && (e.jQuery.LS = e.LS)
	}(window)
}, function (e, t, n) {
	"use strict";
	var r = window.location;
	e.exports = {
		get: function (e) {
			var t = new RegExp("[?&]" + e + "=([^&]*)").exec(r.search);
			return t && decodeURIComponent(t[1].replace(/\+/g, " "))
		}
	}
}, function (e, t, n) {
	"use strict";

	function r(e, t) {
		if (!(e instanceof t)) throw new TypeError("Cannot call a class as a function")
	}

	var i = function () {
			function e(e, t) {
				for (var n = 0; n < t.length; n++) {
					var r = t[n];
					r.enumerable = r.enumerable || !1, r.configurable = !0, "value" in r && (r.writable = !0), Object.defineProperty(e, r.key, r)
				}
			}

			return function (t, n, r) {
				return n && e(t.prototype, n), r && e(t, r), t
			}
		}(),
		o = ["Baiduspider", "Googlebot", "360Spider", "haosouspider", "YodaoBot", "YoudaoBot", "Sosospider", "Yahoo! Slurp", "msnbot", "bingbot", "ia_archiver", "Yisouspider"],
		a = function () {
			function e() {
				r(this, e), this.UA = window.navigator.userAgent
			}

			return i(e, [{
				key: "isSpider", value: function () {
					for (var e = !1, t = 0; t < o.length; t++) if (this.UA.indexOf(o[t]) > -1) {
						e = !0;
						break
					}
					return e
				}
			}]), e
		}();
	e.exports = new a
}, function (e, t, n) {
	"use strict";
	var r = n(13), i = [];
	e.exports = function (e) {
		return function (e, t, n) {
			for (var o = document.querySelector(e), a = 0; a < i.length; a++) if (i[a].player === o) {
				i[a].destroy(), i.splice(a, 1);
				break
			}
			i.push(new r(this, o, t || {}, n))
		}
	}
}, function (e, t, n) {
	"use strict";

	function r(e, t) {
		return Object.prototype.hasOwnProperty.call(e, t)
	}

	e.exports = function (e, t, n, o) {
		t = t || "&", n = n || "=";
		var a = {};
		if ("string" != typeof e || 0 === e.length) return a;
		var s = /\+/g;
		e = e.split(t);
		var u = 1e3;
		o && "number" == typeof o.maxKeys && (u = o.maxKeys);
		var c = e.length;
		u > 0 && c > u && (c = u);
		for (var l = 0; l < c; ++l) {
			var d, p, f, v, h = e[l].replace(s, "%20"), y = h.indexOf(n);
			y >= 0 ? (d = h.substr(0, y), p = h.substr(y + 1)) : (d = h, p = ""), f = decodeURIComponent(d), v = decodeURIComponent(p), r(a, f) ? i(a[f]) ? a[f].push(v) : a[f] = [a[f], v] : a[f] = v
		}
		return a
	};
	var i = Array.isArray || function (e) {
		return "[object Array]" === Object.prototype.toString.call(e)
	}
}, function (e, t, n) {
	"use strict";

	function r(e, t) {
		if (e.map) return e.map(t);
		for (var n = [], r = 0; r < e.length; r++) n.push(t(e[r], r));
		return n
	}

	var i = function (e) {
		switch (typeof e) {
			case"string":
				return e;
			case"boolean":
				return e ? "true" : "false";
			case"number":
				return isFinite(e) ? e : "";
			default:
				return ""
		}
	};
	e.exports = function (e, t, n, s) {
		return t = t || "&", n = n || "=", null === e && (e = void 0), "object" == typeof e ? r(a(e), function (a) {
			var s = encodeURIComponent(i(a)) + n;
			return o(e[a]) ? r(e[a], function (e) {
				return s + encodeURIComponent(i(e))
			}).join(t) : s + encodeURIComponent(i(e[a]))
		}).join(t) : s ? encodeURIComponent(i(s)) + n + encodeURIComponent(i(e)) : ""
	};
	var o = Array.isArray || function (e) {
		return "[object Array]" === Object.prototype.toString.call(e)
	}, a = Object.keys || function (e) {
		var t = [];
		for (var n in e) Object.prototype.hasOwnProperty.call(e, n) && t.push(n);
		return t
	}
}, function (e, t, n) {
	"use strict";
	t.decode = t.parse = n(21), t.encode = t.stringify = n(22)
}, function (e, t, n) {
	var r = n(25), i = n(9), o = i;
	o.v1 = r, o.v4 = i, e.exports = o
}, function (e, t, n) {
	function r(e, t, n) {
		var r = t && n || 0, l = t || [];
		e = e || {};
		var d = e.node || i, p = void 0 !== e.clockseq ? e.clockseq : o;
		if (null == d || null == p) {
			var f = a();
			null == d && (d = i = [1 | f[0], f[1], f[2], f[3], f[4], f[5]]), null == p && (p = o = 16383 & (f[6] << 8 | f[7]))
		}
		var v = void 0 !== e.msecs ? e.msecs : (new Date).getTime(), h = void 0 !== e.nsecs ? e.nsecs : c + 1,
			y = v - u + (h - c) / 1e4;
		if (y < 0 && void 0 === e.clockseq && (p = p + 1 & 16383), (y < 0 || v > u) && void 0 === e.nsecs && (h = 0), h >= 1e4) throw new Error("uuid.v1(): Can't create more than 10M uuids/sec");
		u = v, c = h, o = p, v += 122192928e5;
		var g = (1e4 * (268435455 & v) + h) % 4294967296;
		l[r++] = g >>> 24 & 255, l[r++] = g >>> 16 & 255, l[r++] = g >>> 8 & 255, l[r++] = 255 & g;
		var m = v / 4294967296 * 1e4 & 268435455;
		l[r++] = m >>> 8 & 255, l[r++] = 255 & m, l[r++] = m >>> 24 & 15 | 16, l[r++] = m >>> 16 & 255, l[r++] = p >>> 8 | 128, l[r++] = 255 & p;
		for (var w = 0; w < 6; ++w) l[r + w] = d[w];
		return t || s(l)
	}

	var i, o, a = n(8), s = n(7), u = 0, c = 0;
	e.exports = r
}, function (e, t, n) {
	n(2), e.exports = n(2)
}]);
```

