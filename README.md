# obj_loader - a zig obj file loader

This was very rapidly written to provide a simple interface for loading `.obj` files in zig.

At this time I make no garauntees on correctness or performance.

To load an obj, 

```
const obj_loader = @import("path/to/obj_loader.zig");

var contents: ObjContents = obj_loader.loadObj("suzanne.obj", your.favorite.allocator);
defer contents.deinit();
```

The ObjContents contains a list of ObjMesh objects.

```
std.debug.print("obj: {s}, Vertices count = {d} Normals count = {d}, faces = {d}\n", .{
    contents.meshes.items[0].object_name,
    contents.meshes.items[0].v_positions.items.len,
    contents.meshes.items[0].v_normals.items.len,
    contents.meshes.items[0].v_faces.items.len,
});
```

```
pub const ObjMesh = struct {
    object_name: []u8,
    v_positions: ArrayListUnmanaged(ObjVec) = .{},
    v_colors: ArrayListUnmanaged(ObjColor) = .{},
    v_normals: ArrayListUnmanaged(ObjVec) = .{},
    v_textures: ArrayListUnmanaged(ObjVec2) = .{},
    v_faces: ArrayListUnmanaged(ObjFace) = .{},

    ...
}
```
