# SPIRV-Layout

This library parses SPIRV binaries and retrieves reflection info.
It is most useful for deriving a Vulkan `DescriptorSetLayout` from a shader module, as well as finding offsets and names of individual fields in the Uniform Buffers of a shader.

This crate is used by the [vulkan-engine](https://github.com/michidk/vulkan-engine).

## Usage

```Rust
let bytes = std::fs::read(PATH).unwrap();
let words = unsafe { slice::from_raw_parts(bytes.as_ptr() as *const u32, bytes.len() / 4) };
let module = Module::from_words(words).unwrap();

println!("=== UNIFORMS ===");
for var in module.get_uniforms() {
    print_var(&module, var);
}

println!("=== PUSH CONSTANTS ===");
for var in module.get_push_constants() {
    print_var(&module, var);
}
```

For an actual usage example, see [`examples/reflect-shader`](examples/reflect-shader/main.rs)
