```base
filters:
  and:
    - file.path.startsWith("03 - Case Studies")
    - file.name != "Case Studies"
    - file.path.endsWith(".md")
properties:
  file.name:
    displayName: Case Study
views:
  - type: table
    name: Table
    order:
      - file.name
      - file.backlinks
      - file.embeds
      - file.links
      - file.tags
      - Asked at
      - Difficulty
      - Real-life examples
      - Source
      - Time
    sort: []
    columnSize:
      file.links: auto

```