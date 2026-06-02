# tiny-ecs

Tiny ECS. Archetype-based storage, queries, systems. Zero dependencies. Add entities, attach components, run systems.

## Quick Start

```rust
use tiny_ecs::*;

let mut world = World::new();

let player = world.spawn();
world.add_component(player, Component::Position(0.0, 0.0, 0.0));
world.add_component(player, Component::Velocity(1.0, 0.0, 0.0));
world.add_component(player, Component::Health(100.0));

let mut movement = MovementSystem;
movement.run(&mut world, 1);

let moving = world.query(
    ComponentMask::new()
        .with(ComponentType::Position)
        .with(ComponentType::Velocity),
);
assert_eq!(moving.len(), 1);
```

## Features

- **Entity management** — spawn/despawn with auto-incrementing IDs
- **13 component types** — Position, Velocity, Health, Collider, and more
- **Bitmask queries** — O(1) per-entity mask test
- **Built-in systems** — Movement, Vibe propagation, Collision detection
- **Collision detection** — Circle–Circle, AABB–AABB, Circle–AABB, Point
- **Serialization** — Full serde support, round-trip tested

## License

MIT OR Apache-2.0
