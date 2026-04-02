# FreeSO Remeshes

Hand-authored graphics for [FreeSO](https://github.com/riperiperi/FreeSO) and [Simitone](https://github.com/riperiperi/Simitone)'s 3D mode, made to replace the meshes automatically generated from sprite graphics.

See Releases for the latest remesh package for either FreeSO or Simitone, built off of the main branch.

_NOTE: as of right now, the automatic packager is not active_

## About

Over FreeSO and Simitone's lifespan, remeshes were published by many users to the remeshing forum category: https://forum.freeso.org/forums/3d-remeshing.40/

These were manually packaged and distributed by the FreeSO launcher, which would dump them in the `Content/MeshReplace` folder as loose files. This folder contained an `fsom` file for every DRRP mesh, and `.png` for each mesh texture, which added up to a huge number of files and textures that could decode a bit slowly and take up a lot of VRAM.

This project uses GitHub Actions CI to package into a single DBPF file that the game can keep open and read from much faster. It also supports GPU texture compression (DXT1/DXT5), which greatly reduces the VRAM usage when a lot of remeshes are loaded.

## Folder Structure

- `remeshes/`
  - Contributor name, eg `riperiperi/`
    - `metadata.json` - Information about the author.
    - _(optional)_ `LICENSE.txt` - license for all remesh groups by this author. See License section below for more info.
    - Remesh group name, eg `Flood/`, `Apple Tree/`
      - Remesh files go into this folder, eg. `bball_iff_100.fsom` `bball_iff_TEX_100.png`
      - `metadata.json` - Information about the package.
      - _(optional)_ `Source/` - Source files for the remesh, such as `.blend`, `.psd` projects for the model and textures. You can also include text documents in here if you want to explain more about the process, inspirations etc.
      - _(optional)_ `alt_<variant_name>/` - A variation of the remesh that shouldn't be packaged by default. For example: a Christmas themed version of the parrot.

### Metadata
Metadata automatically populates the credits in the FreeSO client for users with the package installed. Meshes are listed under the creator in the order that they appear in the package.

It also helps people understand what inspired the remesh, the creative liberties taken when authoring it, and what unique problems it solves.

### Creator Metadata

`metadata.json` in the creator folder. Names the creator, includes relevant links and a small optional description.

Feel free to make PRs to update this metadata without any mesh changes.

```json
{
  "name": "riperiperi", // Name to appear on the credits
  "thread": "https://forum.freeso.org/threads/path-of-least-resistance-flood-pack.6261/", // (optional) Thread on the FreeSO forums where the remeshes where originally posted.
  "url": "https://github.com/riperiperi/", // (optional) URL for the most relevant way to contact the creator or see their other work.
  "description": "FreeSO Lead Developer. My remeshes tend to be high-impact and low-effort - typically quick fixes for objects that appear very often or appear entirely broken when generated. I have a focus on keeping the 3D appearance as close to the sprite as possible. I don't have much experience texturing, so all my remeshes use the sprite graphics from the object, rather than custom textures."
}
```

### Package Metadata

`metadata.json` in the package folder. Names the package, includes a link to its source, gives it a small optional description and includes some configuration that affects how it's packaged.

```json
{
  "name": "Flood",
  "description": "Remeshes for all joining tiles of flood.iff. This pack simply projects the original flood sprite onto a plane, with some UV stretching tricks to help it seamlessly tile.", // (optional)
  "url": "", // (optional) URL for the original remesh thread.
  "game": "freeso", // (optional) Set to `freeso` or `simitone` if exclusive to either game. Set to `none` for a full exclusion.
  "priority": 1, // (optional) Resolves file conflicts by choosing files with a higher priority. Defaults to 0.
}
```

## Contributing

The best way to contribute is to fork & clone this project, add your new remesh groups to it, then make a pull request here from your fork. Make sure to follow the file/folder structure above. The contribution can be reviewed here and will be merged if it meets the guidelines below.

### Creating Remeshes
Check out the pinned threads on the FreeSO Forums to learn more about 3D remeshing from scratch, and more complicated features such as depth masks:

- [3D Remeshing basics: Remeshing an object from scratch tutorial](https://forum.freeso.org/threads/3d-remeshing-basics-remeshing-an-object-from-scratch-tutorial.6294/)
- [Depth Masks, Portals and You (for counter sinks, fireplaces)](https://forum.freeso.org/threads/depth-masks-portals-and-you-for-counter-sinks-fireplaces.6377/)

For a more technical overview, check out the written by myself on the FreeSO wiki:
https://github.com/riperiperi/FreeSO/wiki/3D-Remeshing

### Guidelines

The goal of the remesh package is to create appropriate drop-in replacements for meshes automatically generated from the ingame sprites (using their z-buffers).

They should look relatively sharp when zooming in with the camera in 3D mode, and ideally also when in Direct Control mode. They should closely match the position, shape and appearance of the sprite so that rotating with Hybrid 2D/3D mode doesn't look too jarring, though this was not a concern for earlier remeshes.

Ideally, meshes should attempt to bake indirect lighting (ambient occlusion) into their textures, as FreeSO's lighting is rather simple and can't do anything outside of diffuse shading.

Remeshes that significantly change an object's appearance won't be accepted. You can include optional remeshes in `alt_<variant_name>` subfolders in the remesh group, but they won't be included in the default packages.

### Attribution

As you can see in the file structure above, remeshes come in groups, which belong to a primary creator. `metadata.json` in both the creator and group folders provide them display names, which allow any loaded remesh to appear under its creator in the in-game credits.

If you have any additional credits for a remesh, such as it being based off of another remesh or using a texture by someone else, include a `description` with the relevant information.

### Licensing
By default, you should consider all remeshes in this repository under full control of their authors. It's only safe to assume that the meshes collected over the years were shared with the intent of being distributed for FreeSO or Simitone, so if you wish to use them for anything else or modify them in any way, you should contact their creator to check if they're fine with that.

Creators can supply their own license for their remeshes by adding a `LICENSE.txt` file to their contributions folder. This is recommended for new contributions, though you can similarly omit the license to reserve all rights.

If you have remeshes in this repository and you wish to grant or revoke liberties surrounding it, feel free to make a GitHub Issue stating your desired license or simply make a pull request to add it yourself.

### AI Generated Content

_No remeshes included in this package have AI generated content._ Remeshing is and has been a great opportunity for people to learn skills related to 3D modelling and texturing with low stakes and a clear goal - it would be a waste to give up that learning experience to a plagarism machine.

**We will not accept contributions with AI generated content.**