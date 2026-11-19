# Design

Use this directory for material that describes how BINO Care is designed and how its parts fit together. Add files and subdirectories as the design develops.

```text
design/
├── system/      # Whole-system overview and architecture
├── software/    # Platform, UI, and AI designs
│   └── diagrams/ # Software diagrams
├── hardware/    # Hardware design and device details
├── interfaces/  # Connections and data exchanged between parts
└── decisions/   # Significant design choices and their reasons
```

Examples of material to keep here:

* System architecture and component diagrams
* User flows, wireframes, and interface mockups
* Data models, schemas, and API definitions
* Hardware layouts, wiring diagrams, and device interactions
* Deployment and network diagrams

## Diagram tools

* Use **draw.io (diagrams.net)** for visual diagrams such as system architecture, hardware layouts, and user flows. Save each diagram as a single `.drawio.svg` file with the diagram data embedded. The SVG can be viewed as an image and reopened for editing in draw.io. The [draw.io VS Code integration](https://www.drawio.com/docs/integrations/embed-diagrams-vscode/) can edit `.drawio.svg` files directly.
* Use **Mermaid** for diagrams that are easier to maintain as text, such as simple flowcharts and sequence diagrams. Put the Mermaid source in a Markdown file using a `mermaid` code block.

For other design assets, keep an editable version when possible so the team can update them later.
