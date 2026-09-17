# Tech Notes

These are the technical notes I am preparing for my own learning journey. I am sharing them because they may also help other students and developers learning Java and related technologies.

The notes are plain Markdown files, so you can read them directly on GitHub or use them as an [Obsidian](https://obsidian.md/) vault for a better reading and navigation experience.

## What I use

- **Obsidian** — to write, organize, link, and read the Markdown notes.
- **Explorer Order Editor** by [vcarus](https://github.com/vcarus/obsidian-explorer-order-editor) — to manually arrange folders and notes in the Obsidian File Explorer.

The custom order is stored in `explorer-order.md` at the root of this repository. The personal `.obsidian` configuration folder is intentionally not included, because it can contain device-specific workspace settings and locally installed plugin files.

## Set up these notes in Obsidian

### 1. Download the notes

Choose either method:

**Using Git**

```bash
git clone https://github.com/siddhardha-reddy-k/Tech_Notes.git
```

**Without Git**

1. Open this repository on GitHub.
2. Select **Code** and then **Download ZIP**.
3. Extract the downloaded ZIP file to a location you can easily find.

### 2. Install Obsidian

1. Download Obsidian from [obsidian.md/download](https://obsidian.md/download).
2. Install and open the application.

### 3. Open the downloaded folder as a vault

1. On Obsidian's startup screen, select **Open folder as vault**.
2. Browse to the downloaded or cloned `Tech_Notes` folder.
3. Select that folder and choose **Open**.
4. If Obsidian asks whether you trust the author of the vault, review the contents and continue only if you are comfortable doing so.

You can now browse and read all notes. Obsidian will create a new local `.obsidian` folder for your own settings; Git ignores this folder.

### 4. Install Explorer Order Editor (recommended)

The notes work without this plugin, but installing it displays folders and files in the intended custom order.

1. In Obsidian, open **Settings**.
2. Select **Community plugins**.
3. Turn on community plugins if Obsidian asks you to enable them.
4. Select **Browse**.
5. Search for **Explorer Order Editor**.
6. Select the plugin by **vcarus**, choose **Install**, and then choose **Enable**.
7. Return to the File Explorer. The plugin will read `explorer-order.md` and apply the saved ordering.

No additional plugin configuration is required for the saved order.

## Keeping your copy up to date

If you cloned the repository with Git, open a terminal inside the `Tech_Notes` folder and run:

```bash
git pull
```

If you downloaded a ZIP, download a new copy whenever you want the latest notes.

## A note about the content

These are personal learning notes and may continue to change as I learn. They are intended as study material, not as official documentation. If you find an error or have a useful improvement, feel free to open an issue or submit a pull request.
