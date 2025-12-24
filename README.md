# arch-waypure

**arch-waypure** is a curated collection of Arch Linux PKGBUILDs designed to create a **clean, modern Wayland-only** environment. The goal of this project is to focus on **minimalism**, **performance**, and **security**, while providing packages optimized for a native Wayland setup.

The packages in **arch-waypure** are built with the following key principles:

- **Wayland-only**: No dependencies on X11, Xorg, or XWayland.
- **PipeWire-only**: Audio handled exclusively by PipeWire, with no support for PulseAudio or JACK.
- **Vulkan/EGL**: Prefer Vulkan and EGL for graphics rendering whenever possible, with OpenGL/GLX being a secondary option.
- **Minimalism**: Avoid unnecessary legacy features, compatibility layers, and bloat.
- **Reproducible builds**: Packages are built from official release `.tar.gz` archives or official upstream git sources.
- **Efficient and fast builds**: A streamlined process designed for quick and reproducible builds.

## Key Features

- **Wayland-only**: No reliance on X11 or XWayland.
- **PipeWire-only**: Exclusively uses PipeWire for audio handling.
- **Vulkan/EGL**: Prefer Vulkan/EGL over older OpenGL/GLX implementations.
- **Minimal dependencies**: Only include the essential packages required for a Wayland-based environment.
- **Reproducible builds**: Ensuring that the build process is both reliable and repeatable.

## Supported Categories

- **Graphics**: Includes Vulkan, EGL, Mesa, and related packages.
- **Wayland**: Compositors, protocols, utilities (e.g., Sway, wlroots, Wayfire).
- **Apps**: Wayland-compatible applications (e.g., foot terminal, grim).
- **Utilities**: Essential tools for a Wayland-based environment (e.g., wlr-randr).

## Package Organization

Instead of having separate subfolders for different categories, each package is located under its own directory, named after the package. The structure is simplified:

```bash
arch-waypure/
├── wlroots/
│   ├── PKGBUILD
│   └── .SRCINFO
├── sway/
│   ├── PKGBUILD
│   └── .SRCINFO
└── foot/
    ├── PKGBUILD
    └── .SRCINFO
````

### Example of a typical package directory:

Each package should contain the following:

```sh
pkgname/
├── PKGBUILD
├── .SRCINFO
└── optional.patch  # (only if necessary)
```

To generate the `.SRCINFO` file after editing the `PKGBUILD`:

```sh
makepkg --printsrcinfo > .SRCINFO
```

## How to Contribute

To contribute to **arch-waypure**, please read the [Contributing Guidelines](CONTRIBUTING.md) for full instructions.

We encourage contributions that align with the project's core principles. Packages should meet the following criteria:

- **Wayland-only**: The package must run natively with Wayland (no X11 or XWayland dependencies).
- **PipeWire-only**: The package must route audio through PipeWire (no PulseAudio or JACK).
- **Vulkan/EGL preferred**: Prefer Vulkan or EGL for graphics; avoid legacy OpenGL/GLX support unless absolutely necessary.
- **Minimal dependencies**: Only include essential dependencies.
- **Reproducibility**: Ensure the build process is reproducible.

### How to Build a Package

To build any package from **arch-waypure**, follow these steps:

1. Clone the repository:

   ```sh
   git clone https://github.com/<your-username>/arch-waypure.git
   cd arch-waypure
   ```

2. Navigate to the package directory:

   ```sh
   cd arch-waypure/<pkgname>
   ```

3. Build the package:

   ```sh
   makepkg -si
   ```

4. For a **clean chroot** build (recommended for reproducibility):

   ```sh
   extra-x86_64-build
   ```

5. Optionally, run `namcap` to lint the PKGBUILD and package:

   ```sh
   namcap -i PKGBUILD
   namcap -i *.pkg.tar.zst
   ```

## Licensing

The **PKGBUILDs** in this repository are licensed under **0BSD**, unless otherwise specified. Refer to upstream licenses for the software runtime.

## Issues & Discussions

- **Issues**: Use the issue tracker for bug reports, packaging problems, or feature requests.
- **Pull Requests**: Submit pull requests for new packages, refactoring, or improvements.
- **Discussions**: Use GitHub discussions for non-technical topics, ideas, or questions.

## Thank You

Thank you for contributing to **arch-waypure**! Your contributions help build a more modern, minimal, and efficient Linux ecosystem. Together, we're pushing forward a Wayland-native future for Arch users.
