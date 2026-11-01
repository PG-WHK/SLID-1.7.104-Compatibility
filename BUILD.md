# SLID compatibility source

Upstream: https://github.com/ohfor/slid at c630dba767fd5d0cadb7903d3fa08e377deb86ef (SLID 1.4.9).
The original mod's ESP, SWF, PEX, INI and Babel files are not distributed here.

Build with Visual Studio 2022 x64 / MSVC 19.44, Windows SDK, CMake 3.21+,
/MD Release and C++23. Install dependency CMake packages into a prefix:
spdlog 1.17.0, fmt 12.2.0 and DirectXTK May 2026; provide rapidcsv 9.07,
DirectXMath June 2026 and SimpleIni 4.27 headers. Sources are in third_party.

    cmake -S SLID -B build -G "Visual Studio 17 2022" -A x64 -DCMAKE_PREFIX_PATH=<dependency-prefix>
    cmake --build build --config Release --target SLID

Bundled CommonLib baseline: 94faaed0c60eddd8347767f2d4d29a97c93bde8c,
with local CMake integration and Address Library format-5 support; AE only.
MinHook baseline: c3fcafdc10146beb5919319d0683e44e3c30d537.
The distributed trial binary links the matching prebuilt local CommonLib;
the source configuration builds CommonLib from its corresponding source.
Binary-identical rebuilds are not promised. No automatic game/MO2 installation.

Changes: see SLID-compatibility.patch and the binary README. Manual game test passed for the scope described in README.md.
