# OpenDRT — GLSL Implementation

A single-file GLSL port of [OpenDRT](https://github.com/jedypod/open-display-transform), a professional, open-source Display Rendering Transform. Designed for real-time use in graphics applications and video games. Other ports can be found here as well.

## Quick Start

**1. Include the file** in your shader (via `#include` or by pasting the source):

```glsl
#include "opendrt.glsl"
```

**2. Call `opendrt()`** from your fragment shader:

```glsl
#version 330 core

in vec2 tex_coords;
out vec4 frag_color;
uniform sampler2D screen_texture; // Linear Rec.709 input

// #include "opendrt.glsl" or source added here...

void main() {
    vec3 color = texture(screen_texture, tex_coords).rgb;

    // Start with a preset.
    OpenDRTParams opendrt_params = OPENDRT_PARAMS_STANDARD;

    // Optionally override individual parameters.
    // opendrt_params.tn_Lp  = 1000.0; // Target 1000-nit HDR display
    // opendrt_params.tn_con = 1.8;   // More contrast

    // Apply the OpenDRT transform.
    color = opendrt(color, opendrt_params);

    // Apply display EOTF.
    color = pow(color, vec3(1.0 / 2.2));

    frag_color = vec4(color, 1.0);
}
```

## Acknowledgements

This implementation is a GLSL port of [OpenDRT by Jed Smith](https://github.com/jedypod/open-display-transform). All core algorithms, parameter semantics, and preset values originate from that project. Please refer to the upstream repository for the full technical specification, discussion, and reference implementations for DaVinci Resolve and Nuke.

## License

[GPL v3](https://github.com/JElfferich/OpenDRT/blob/main/README.md)
