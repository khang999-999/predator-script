/*
╔══════════════════════════════════════════════╗
║        PREDATOR ELITE X V12 ULTRA           ║
║      SHADOWROCKET / SURGE / LOON            ║
╚══════════════════════════════════════════════╝
*/

const PREDATOR = {

    VERSION: "12.0 ULTRA",

    AUTH_KEY: "KHANG_PREDATOR_X",

    TOUCH: {
        RESPONSE: 1.35,
        SWIPE_SMOOTH: 0.95,
        TOUCH_LATENCY: 0.0025,
        DRAG_ACCURACY: 1.20,
        REDUCE_STICKNESS: true,
        SMART_TOUCH: true
    },

    NETWORK: {
        LOW_LATENCY: true,
        STABLE_PING: true,
        PACKET_PRIORITY: "ULTRA",
        DNS_BOOST: true,
        ANTI_SPIKE: true
    },

    PERFORMANCE: {
        FPS_BOOST: true,
        FRAME_STABLE: 0.98,
        GPU_BALANCE: 0.90,
        MEMORY_CLEANER: true,
        THERMAL_CONTROL: true,
        CPU_STABILIZER: true
    },

    VISUAL: {
        SHADOW_REDUCE: true,
        RENDER_OPTIMIZE: true,
        PARTICLE_REDUCE: true
    }
};

/* =========================================
   ENCRYPT
========================================= */

function dynamicAuth() {

    const ts = Math.floor(Date.now() / 1000);

    let out = "";

    for (let i = 0; i < ts.toString().length; i++) {

        let enc =
            (
                ts.toString().charCodeAt(i) ^
                PREDATOR.AUTH_KEY.charCodeAt(
                    i % PREDATOR.AUTH_KEY.length
                )
            ) + 25;

        out += ("0" + enc.toString(16)).slice(-2);

    }

    return `${ts}.${out}`;
}

/* =========================================
   RANDOMIZER
========================================= */

function rand(min, max) {

    return (
        Math.random() * (max - min) + min
    ).toFixed(3);

}

/* =========================================
   REQUEST
========================================= */

async function onRequest(req, script) {

    let h = req.headers;

    // AUTH
    h["X-PREDATOR-AUTH"] = dynamicAuth();

    // NETWORK
    h["X-Low-Latency"] = "true";
    h["X-Stable-Ping"] = "enabled";
    h["X-Anti-Spike"] = "true";

    // TOUCH
    h["X-Touch-Boost"] =
        PREDATOR.TOUCH.RESPONSE.toString();

    h["X-Swipe-Smooth"] =
        PREDATOR.TOUCH.SWIPE_SMOOTH.toString();

    h["X-Reduce-Stickness"] = "true";

    // PERFORMANCE
    h["X-FPS-Boost"] = "enabled";
    h["X-GPU-Stable"] = "true";
    h["X-Memory-Cleaner"] = "true";

    console.log("🚀 PREDATOR REQUEST ACTIVE");

    return req;
}

/* =========================================
   RESPONSE
========================================= */

async function onResponse(req, resp, script) {

    if (!resp) return resp;

    const url = req.url;

    /* =====================================
       BLOCK DETECT
    ===================================== */

    if (
        url.includes("CheckHackBehavior") ||
        url.includes("GetMatchmakingBlacklist") ||
        url.includes("report") ||
        url.includes("security") ||
        url.includes("ban") ||
        url.includes("anticheat") ||
        url.includes("/ver/")
    ) {

        resp.statusCode = 403;

        resp.headers["Content-Type"] =
            "text/plain";

        resp.body =
            "[00FF00]PREDATOR ELITE X ACTIVE";

        delete resp.headers["Content-Length"];

        console.log("🛡 DETECT BLOCKED");

        return resp;
    }

    /* =====================================
       JSON MODIFY
    ===================================== */

    try {

        if (
            resp.headers["Content-Type"] &&
            resp.headers["Content-Type"]
            .includes("application/json")
        ) {

            let obj = JSON.parse(resp.body);

            // TOUCH
            obj.touch_response =
                parseFloat(rand(1.25, 1.35));

            obj.touch_latency =
                parseFloat(rand(0.002, 0.004));

            obj.drag_accuracy =
                parseFloat(rand(1.10, 1.20));

            obj.reduce_stickness = true;

            // NETWORK
            obj.low_latency = true;
            obj.stable_ping = true;
            obj.packet_priority = "ULTRA";

            // PERFORMANCE
            obj.fps_boost = true;
            obj.frame_stability =
                parseFloat(rand(0.92, 0.99));

            obj.memory_cleaner = true;
            obj.thermal_control = true;

            // VISUAL
            obj.shadow_reduce = true;
            obj.render_optimize = true;

            resp.body = JSON.stringify(obj);

            delete resp.headers["Content-Length"];

            console.log("⚡ RESPONSE MODIFIED");

        }

    } catch (e) {

        console.log("❌ MODIFY FAILED");

    }

    return resp;
}

