# Flatpak extension generator for Kolibri channels

This repo is used to create [Flatpak extensions](https://github.com/flatpak/flatpak/wiki/Extensions) with Kolibri content that, once installed, the [Flatpak Kolibri client](https://github.com/learningequality/org.learningequality.Kolibri) can use it through the `KOLIBRI_CONTENT_FALLBACK_DIRS` environment variable as it was imported to the Kolibri device.

## Usage

You can generate as many extensions as you like with the combination of content you desire.

Let say we want to generate an extension for content of *Khan Acadamey (English)*, whose ID is `1ceff53605e55bef987d88e0908658c5` and we want all the content from the *Resources* topic, whose ID is `c4b7fbced0815809a1f7ed411f49cd9c`.

We also have to choose an ID for the extension, which is going to be appended to `org.learningequality.Kolibri.Content`, let say, `Khan_en_Resources`

The first step is to run `generate-manifest` command that will import the content in a temporary Kolibri Home directory, generate the Flatpak manifest and the AppStream file:

```sh
./generate-manifest --id Khan_en_Resources --channel="channel_id=1ceff53605e55bef987d88e0908658c5:node_ids=c4b7fbced0815809a1f7ed411f49cd9c"
```

You can also create an extension from the data inside the `extensions-catalog.json` file, you just need to specify the ID:

```sh
./generate-manifest --id ID_From_The_Catalog
```

Any other options passed to that command will override what's on `extensions-catalog.json` except for the channels (they are going to be appended).

**Note:** run `./generate-manifest -h` for more information on how to use this command.

Now you can build the Flatpak as you usually do:

```sh
flatpak-builder build manifest.json
```

**Note:** add `--install --user` flags to install the extension right away after building it.
