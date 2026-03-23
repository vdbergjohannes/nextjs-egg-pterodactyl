# 🚀 Next.js Pterodactyl Egg (Network Binding Fix)

A custom, optimized Pterodactyl Egg for hosting **Next.js** applications.

This version resolves the common connectivity issue where Next.js servers show as "Ready" in the console but remain inaccessible via the browser/IP address due to incorrect network binding.

## 🧐 The Problem & Solution
By default, Next.js applications often bind to `localhost` (127.0.0.1). Inside a Docker container (which Pterodactyl uses), this prevents the application from being accessible from the outside world.

**This Egg fixes that** by automatically forcing the start command to listen on all interfaces (`0.0.0.0`), ensuring your site is immediately accessible after deployment.

It also improves startup reliability by using smarter dependency install behavior with package manager detection:

* `auto` mode detects lockfiles and picks `pnpm`, `yarn`, or `npm` automatically.
* In `start` mode, it installs production dependencies and builds before launch.
* In `dev` mode, it installs full dependencies so local development tools still work.

---

## 🧩 Supported Versions

This Egg comes pre-configured with **all modern Node.js versions**, selectable during installation:

* **Node.js 25** (Latest)
* **Node.js 24** (LTS)
* **Node.js 23**
* **Node.js 22** (LTS)
* **Node.js 21**
* **Node.js 20** (LTS)
* **Node.js 19**
* **Node.js 18** (LTS)

✅ **Next.js Compatibility:** Supports all modern Next.js versions (13, 14, 15, 16+) that run on these Node environments.

---

## ✨ Features

* **🔌 Instant Connectivity:** Pre-configured to listen on `0.0.0.0`, solving connection timeouts.
* **📦 Auto-Install:** Automatically runs `npm install` on startup if packages are missing.
* **⚙️ Smart Build:** Runs `npm run build` automatically in production mode (`NODE_RUN_ENV=start`).
* **🧠 Package Manager Auto-Detect:** Supports `npm`, `pnpm`, and `yarn` with optional manual override.
* **🔒 Secure:** Based on the official Pterodactyl Docker images (Parkervcp/Yolks).
* **✅ Better Validation:** Restricts runtime mode to `start` or `dev` to prevent invalid command values.

## 🔧 Recommended Variables

* `NODE_RUN_ENV`: `start` for production, `dev` for development.
* `PACKAGE_MANAGER`: `auto` (default), `npm`, `pnpm`, or `yarn`.

## 📥 Installation Guide

1.  **Download:** Get the `nextjs-egg.json` file from this repository (or copy the RAW link).
2.  **Import:** Go to your **Pterodactyl Admin Panel** -> **Nests** -> **Import Egg**.
3.  **Select Nest:** Choose the appropriate Nest (usually "NodeJS" or "Generic").
4.  **Upload:** Upload `nextjs-egg.json` and complete the import wizard.
5.  **Deploy:** You can now create new servers using this Egg!

> **Auto-Update:** This Egg is configured with an `update_url` pointing to the latest version on GitHub. You can update it in your panel via **Admin** -> **Nests** -> select the egg -> **Update from URL**.

---

## 🛠️ Troubleshooting

* **Install fails with package manager errors:** Set `PACKAGE_MANAGER` manually to `npm`, `pnpm`, or `yarn` instead of `auto`.
* **`pnpm` or `yarn` command not found:** Keep `PACKAGE_MANAGER=npm` or ensure Corepack is available in your selected Node image.
* **Unexpected dependency behavior:** Verify lockfiles in your project root (`package-lock.json`, `pnpm-lock.yaml`, or `yarn.lock`).
* **Server builds on every boot in production:** This is expected when `NODE_RUN_ENV=start`; use `dev` while iterating quickly.
* **Server not reachable from outside:** Confirm your panel allocation/port is correct; this Egg already binds Next.js to `0.0.0.0`.

---

## ☕ Support My Work

If this Egg saved you time or fixed your server headaches, consider supporting my work! It helps me keep creating tools and fixes.

* **PayPal:** [paypal.me/JoopDev](https://www.paypal.me/joopdev)
* **Website:** [JoopDev.com](https://joopdev.com)

---

**Author:** JoopDev (AKA. Vdbergjohannes)
