# Contributing to arch-waypure

Thank you for your interest in contributing to **arch-waypure**, a collection of Arch Linux PKGBUILDs focused on building a **clean, modern, Wayland-native** environment. This project prioritizes **minimalism**, **performance**, and **security**, providing packages optimized for a native Wayland setup.

Before submitting a package or pull request, please read and follow these guidelines carefully.

---

## Project Scope

**Packages submitted to arch-waypure must meet these strict criteria:**

- **Wayland-only**: No dependencies on X11, Xorg, or XWayland.
- **PipeWire-only**: Audio handled exclusively by PipeWire, with no support for PulseAudio or JACK.
- **Vulkan/EGL**: Prefer Vulkan and EGL for graphics rendering whenever possible, with OpenGL/GLX being a secondary option.
- **Minimalism**: Avoid unnecessary legacy features, compatibility layers, and bloat.
- **Source-based builds**: Packages are built from **official `.tar.gz` releases** or official upstream git sources.
- **Reproducible builds**: Packages must be reproducible and efficient.

---

## Package Submission Guidelines

### ✅ What you should do:

- Use **stable release tarballs** (`.tar.gz`) as your source.
- Minimize package dependencies to only what's strictly necessary for a Wayland environment.
- **Patch only when required**: Only patch when necessary (e.g., for build issues, security updates, or minimal support).
- Ensure all packages are **Wayland-only** and **PipeWire-only**.
- Use **sha256sums** for file integrity verification in your `PKGBUILD`.
- Declare any build-specific arguments (such as `_meson_options`, `_cmake_options`, or `_make_options`) in the `build()` function. These should be clearly stated and passed to the respective build systems for clarity and consistency.
- Test all packages in a **clean chroot or container** environment (see [clean chroot setup](https://wiki.archlinux.org/title/DeveloperWiki:Building_in_a_clean_chroot)).
- Follow the [Arch Linux packaging standards](https://wiki.archlinux.org/title/Arch_package_guidelines).

### ❌ What you should **NOT** do:

- Do **not** submit packages that depend on:
  - X11 (e.g., `libX11`, `xorg`, `xwayland`, etc.).
  - PulseAudio, JACK (unless routed through PipeWire).
  - Deprecated toolkits like **GTK 2**, **Qt 4**, or other legacy dependencies.
- Avoid using **git** sources unless absolutely necessary, and ensure they are from **official repositories** (not personal forks).
- Do not add **optional features** that violate the project’s minimalism, security, or Wayland/PipeWire principles.
- Avoid submitting graphical applications that require **XWayland** to function.

---

## Build Guidelines

### Declaring Build Options

When defining the build process in your `PKGBUILD`, you should declare any build-specific options such as:

- `_meson_options`
- `_cmake_options`
- `_make_options`

For example, in the `build()` function, the declaration of `meson` build options might look like this:

```bash
build() {
  local _meson_options=(
    -D some_feature=auto
  )

  arch-meson "${pkgname%%-*}-$pkgver" build "${_meson_options[@]}"
  
  meson compile -C build
}
```

This ensures that build options are clearly defined and passed to the respective build system (Meson, CMake, or Make), improving clarity and maintainability.

### Using `sha256sums`

All sources in your `PKGBUILD` must use `sha256sums` for integrity verification. This ensures the authenticity of the source code and prevents issues with corrupted or modified downloads.

For example:

```bash
source=("https://example.com/package-$pkgver.tar.gz")
sha256sums=('1234567890abcdef1234567890abcdef1234567890abcdef1234567890abcdef')
```

Ensure that the correct checksum is used and re-validate it before submitting the package.

---

## File Structure

Each package should be placed directly under its own directory, named after the package. The structure is simplified as follows:

```bash
arch-waypure/
├── wlroots/
│   ├── PKGBUILD
│   ├── .SRCINFO
├── sway/
│   ├── PKGBUILD
│   ├── .SRCINFO
└── foot/
    ├── PKGBUILD
    └── .SRCINFO
```

---

## Build & Linting

To ensure the package is correct, use a **clean chroot** for building:

```bash
extra-x86_64-build
```

To check the quality of your **PKGBUILD** and package, run `namcap`:

```bash
namcap -i PKGBUILD
namcap -i *.pkg.tar.zst
```

---

## Commit Messages

Please follow [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/) for commit messages. Use clear and concise messages with the following format:

```js
<type>(<scope>): <short summary>

<optional longer description>
```

Examples:

```js
add(wlroots): disable xcb support by default
remove(mesa-xlib): drop support for X11-based Mesa variant
update(foot): bump to 1.17.0 release
fix(wlr-randr): disable X11-related build flags
change(wlroots): remove XWayland support entirely
docs: add CONTRIBUTING.md and clarify build steps
cleanup: remove unnecessary patches from sway PKGBUILD
refactor(common): move shared build functions to templates/
security(pipewire): apply CVE-2025-xxxx patch
```

---

## Licensing

The **PKGBUILDs** in this repository are licensed under the **0BSD** license. This is the same license used by Arch Linux, ensuring that all contributions can be freely used and distributed.

Refer to upstream licenses for the software runtime.

---

## Issues & Discussions

- **Issues:** Use the issue tracker for bug reports, packaging problems, or feature requests.
- **Pull Requests:** Submit pull requests for new packages, refactorings, or improvements.
- **Discussions:** Use GitHub discussions for non-technical topics, ideas, or questions.

---

## Thank You!

Thank you for contributing to **arch-waypure**! Your contributions help build a cleaner, more modern, and efficient Linux ecosystem. Together, we're pushing forward a Wayland-native future for Arch users.
