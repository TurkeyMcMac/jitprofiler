# LuaJIT Profiler

This Minetest mod lets you use LuaJIT's builtin profiler. This profiler is good
for pinpointing expensive parts of mod code.

## How to Use

- Add the mod to the `secure.trusted_mods` list.
- Enable the mod.
- In-game start the profiler with `/jitprofiler_start 1 <filename>`. The
  profiling data will be written to `<worldpath>/jitprofiles/<filename>`.
- Collect data for a while.
- Stop profiling with `/jitprofiler_stop` or by exiting the world.
- Download FlameGraph if you haven't done so.
- Create a flame graph SVG with
  `./flamegraph.pl <worldpath>/jitprofiles/<filename> > graph.svg`.
- Open the SVG with your browser or another viewing program.
- The top level of each stack snapshot will be "C", "G", "I", "J", or "N",
  representing C code, garbage collection, interpreter, JIT compilation, or
  compiled code, respectively.

## Issues

- Sometimes a lot of C code execution is reported in suspicious places. I think
  this represents time taken by the Minetest engine, but I don't know why the
  profiler thinks the code is executed inside a Lua function.
- Using this mod with Mesecons luacontrollers can cause crashes for some reason.
