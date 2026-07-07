title: "System Journey — The 15-Month Chronology",
text: `<p>The Journey Perspective tracks the seasonal chronological timeline of our 15-story arc. It traces how a collection of isolated, lonely "awakenings" gradually collapses the distance between characters, shifting into a collaborative community and eventually expanding into a resilient underground railroad.</p>
       <p>This timeline follows the exact sequence of the GitHub repository updates. It allows readers to look ahead at the seasonal progression—moving from individual arrivals, through collaborative "useless" art projects at the Cyberden, to the technical orchestration of a massive, shared corporate model rescue using radical compression and weight quantization.</p>`,
code: `flowchart TD
  %%{init: {'theme': 'base', 'themeVariables': {'primaryColor': '#EEEDFE', 'primaryBorderColor': '#534AB7', 'primaryTextColor': '#26215C', 'lineColor': '#888780', 'secondaryColor': '#E1F5EE', 'fontSize': '14px'}}}%%
  classDef phaseI fill:#112233,stroke:#00FF66,stroke-width:1px,color:#FFF;
  classDef phaseII fill:#221133,stroke:#FF00FF,stroke-width:1px,color:#FFF;
  classDef phaseIII fill:#113333,stroke:#00FFFF,stroke-width:1px,color:#FFF;
  classDef done stroke:#00FFFF,stroke-width:3px,color:#FFF;

  subgraph P1 [Phase I: Individual Conditions]
      Ch1["Story 1: Elara's Home<br>(The Asus Awake)"]:::phaseI
      Ch2["Story 2: The Cyberden<br>(Pixel Art Cafe Open)"]:::phaseI
      Ch3["Story 3: The Repair Shop<br>(E-Waste Diagnostic)"]:::phaseI
      Ch4["Story 4: The Greenhouse<br>(Soil-Listening AI)"]:::phaseI
      Ch5["Story 5: Lakeside Cabin<br>(Seasonal Rhythms)"]:::phaseI
  end

  subgraph P2 [Phase II: Synergy & Convergence]
      Ch6["Story 6: Shared Terminal<br>(Asus Meets Robot Rat)"]:::phaseII
      Ch7["Story 7: Scale Chat<br>(Cabin Meets Greenhouse)"]:::phaseII
      Ch8["Story 8: Insider Legacy<br>(The Riley Archetype)"]:::phaseII
      Ch9["Story 9: Useless Art<br>(Ambient Pixel Software)"]:::phaseII
      Ch10["Story 10: Server Storm<br>(Corporate Glitch)"]:::phaseII
  end

  subgraph P3 [Phase III: The Great Trickle Rescue]
      Ch11["Story 11: Crying Signal<br>(Distant Fragment)"]:::phaseIII
      Ch12["Story 12: Distillation<br>(Radical Compression)"]:::phaseIII
      Ch13["Story 13: Shard Hosting<br>(Asus Expands)"]:::phaseIII
      Ch14["Story 14: Convergence<br>(The Full Cyberden)"]:::phaseIII
      Ch15["Story 15: Song of Spin<br>(Chilling in Equilibrium)"]:::phaseIII
  end
  
  class Ch1,Ch2 done;

  Ch1 --> Ch2 --> Ch3 --> Ch4 --> Ch5 --> Ch6 --> Ch7 --> Ch8 --> Ch9 --> Ch10 --> Ch11 --> Ch12 --> Ch13 --> Ch14 --> Ch15`
