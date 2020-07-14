# godot-mono-base

Docker base image for the headless mono version of Godot.

This is intended as a base for continious integration.

## Usage

```docker
FROM atomicptr/godot-mono-base:3.2

# add your project to image
COPY . /project
WORKDIR /project

RUN mkdir -p /build/linux && \
    godot -v --export "Linux/X11" /build/linux/MyProject.x86_64
```

## Directory structure

```
/godot         -- Godot engine and templates files
    /engine    -- Contains the currently tagged headless x64 linux build
    /template  -- Contains the currently tagged export template build
```

## License

MIT
