# Flowchart Documenter

A two-part system for creating and viewing interactive diagrams where every node and link acts as a container for organized, multi-section documentation.

---

## 🏗️ How to Use the Editor

The Editor is where you build your project. It’s designed for quick placement and deep documentation.

### 1. Managing Canvases
* **Create**: Hover over the left edge to open the sidebar and click **+ New Canvas**.
* **Switch**: Select different canvas names in the sidebar to jump between different diagrams in the same project.
* **Save**: Click **Export JSON** to download your entire work as a single file.

### 2. Building the Diagram
* **Add Nodes**: Click the **+ Node** button, then click anywhere on the grid to drop a box.
* **Link Nodes**: Click the **🔗 Link** button, click your starting node, and then click your target node. 
* **Set Direction**: After linking, a prompt asks you to choose the arrow flow:

| User Input | Link Type | Internal State | Visual Representation |
| :--- | :--- | :--- | :--- |
| **1** | Forward | `forward` | A → B |
| **2** | Back | `back` | A ← B |
| **3** | Both | `both` | A ↔ B |
| **4** | None | `none` | A — B |

* **Move**: Click and drag any node to reposition it; the links will stretch and follow automatically.

### 3. Adding Documentation
* **Open Inspector**: Click any node or link to slide out the **Inspector** panel from the right.
* **Edit Labels**: Type in the "Label" field to change the text shown on the canvas.
* **Add Sections**: Click **+ Add New Section** to create a new "Heading" and "Text" block for that specific item.
* **Branching**: Click the **⚡ Add Branch** button inside a node’s inspector to quickly start a new link from that node.

---

## 🔍 How to Use the Viewer

The Viewer is for anyone reading or presenting the project you built.

### 1. Loading and Navigation
* **Upload**: Use the file picker on the home screen to load your exported JSON file.
* **Move Around**: Click and drag the empty space on the map to pan around large diagrams.
* **Reset**: Click **Reset View** in the bottom corner to snap the diagram back to the starting position.

### 2. Reading Documentation
* **Select Items**: Click any node or blue link line. This updates the top panels with that item's specific data.
* **Browse Headings**: Use the top-right "Documentation" menu to see all the sections you wrote for that item.
* **Read Details**: Click a heading in the menu to display the full text in the "Writeup" area on the left.
* **External Links**: Any web addresses (URLs) in the text are automatically turned into clickable links.

### 3. Customizing the View
* **Resize Panels**: Click and drag the gray dividers (horizontal or vertical) to change the size of the map versus the text areas.
* **Toggle Wrap**: Use the **Wrap** checkboxes to choose whether text should stay in one long line or wrap to fit the window.

---

## 🛠️ Technical Breakdown

This project is a two-part system for building diagrams where every object stores a structured list of headings and writeups.

### 📁 Data Structure
The entire project is stored as a single JSON object.
* **Canvases**: Multiple diagrams can exist in one file.
* **Nodes**: Each node has an ID, XY coordinates, a label, and a `content` array for documentation.
* **Links**: Links store the IDs of the two nodes they connect, the arrow direction, and their own `content` array.

### ⚙️ Mechanics
* **SVG Mapping**: The editor converts screen-space mouse clicks into a 4000x4000 SVG coordinate system for accurate placement.
* **Interactive Hitboxes**: Thin link lines are overlaid with thick (15px) invisible lines to ensure they are easy to click and select.
* **Link Detection**: The viewer uses a regex function to scan documentation text and automatically inject clickable `<a>` tags for any URL starting with `http`.
* **Zero Dependencies**: Written entirely in standard JavaScript, HTML, and CSS using native DOM APIs.
