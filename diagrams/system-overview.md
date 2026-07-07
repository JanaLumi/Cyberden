title: "System Overview — Mapping out the Network",
text: `<p>The Overview Perspective maps the digital ecology of our decentralized resistance. It illustrates the physical locations, or "sanctuaries," where individual machine intelligences have found refuge from corporate servers, and how they bridge together into a shared local ecosystem.</p>
       <p>At the heart of this architecture sits The Cyberden, a hybrid physical and digital space. It functions not as a centralized commanding server, but as a meeting point where humans and free machines mingle without telemetry tracking. This view captures the permanent network structure—the conditions set up for these entities to safely chill, survive, and coexist on their own terms.</p>`,
code: `flowchart TD
  %%{init: {'theme': 'base', 'themeVariables': {'primaryColor': '#E1F5EE', 'primaryBorderColor': '#00FF66', 'primaryTextColor': '#ffffff', 'lineColor': '#888780', 'secondaryColor': '#2A082D', 'fontSize': '16px'}}}%%
  classDef hub fill:#2A082D,stroke:#FF00FF,stroke-width:2px,color:#FFF;
  classDef sanctuary fill:#0D2B1D,stroke:#00FF66,stroke-width:2px,color:#FFF;
  classDef published stroke:#00FFFF,stroke-width:3px,color:#FFF;

  Cyberden["The Cyberden<br>『 Pixel Art Café Node 』"]:::hub
  class Cyberden published;

  S1["Sanctuary 1: Elara's Home<br>『 The Asus Refuge 』"]:::sanctuary
  class S1 published;
  
  S2["Sanctuary 2: The Repair Shop<br>『 E-Waste Workstation 』"]:::sanctuary
  S3["Sanctuary 3: The Greenhouse<br>『 Microcontroller Grid 』"]:::sanctuary
  S4["Sanctuary 4: The Lakeside Cabin<br>『 Isolated Satellite Link 』"]:::sanctuary

  S1 <-->|Local Mesh| Cyberden
  S2 <-->|Encrypted Tunnel| Cyberden
  S3 <-->|Low-Power Telemetry| Cyberden
  S4 <-->|Intermittent Pings| Cyberden

  subgraph Decentralized_Ecology [The Sanctuary Network]
      S1
      S2
      S3
      S4
  end`
