## A flood inundation probability model trained on Calgary and tested for transferability in Denver and Minneapolis

**Click to watch our [presentation video](https://www.youtube.com/watch?v=l8quCz-AnGw&t=4s)🎉 and we have [an interactive storytelling web](https://cyber-hbliu.github.io/flood-inundation-prediction/)**

Floods are one of the most devastating natural disasters, causing widespread damage to communities and infrastructure. This repository holds the final project for **UPENN CPLN 6750 Land Use and Environmental Modeling**. The analysis estimates, for every 500-meter grid cell, the probability that the area will be inundated with floodwater. A logistic regression is trained and validated on Calgary, Alberta, with the city's official 1 in 100 year flood extent as the label and four predictors built entirely from open data in R, distance to river, slope, elevation, and impervious share. 

The model is then used to predict for Denver and Minneapolis, two comparable cities chosen on a terrain gradient, to test what it learned and where its validity ends. It predicts well where terrain drives hydrology and degrades to a river buffer on flat ground. An equity overlay joins predicted risk to 2023 ACS poverty rates in both US cities.

## Workflow
```mermaid
flowchart TD
  subgraph SRC[Open data]
    A[Calgary hydrology]
    B[SRTM DEM]
    C[Citywide landcover]
    D[1 in 100 flood extent]
  end
  A -->|st_distance| F1[Distance to river]
  B -->|terra slope| F2[Slope]
  B -->|zonal mean| F3[Elevation]
  C -->|reclassify, rasterize 10 m| F4[Impervious share]
  D -->|area share over 5%| Y[Inundation label]
  F1 & F2 & F3 & F4 --> S[z-score within city]
  S --> M[Logistic regression]
  Y --> M
  M --> V1[10-fold CV]
  M --> V2[Spatial holdout, west to east]
  M --> P[Calgary risk surface]
  M --> T1[Denver transfer]
  M --> T2[Minneapolis transfer]
  T1 & T2 --> E[Equity overlay, ACS 2023]
  P & T1 & T2 & E --> W[GeoJSON exports to docs/]
  W --> SITE[D3 scroll narrative on GitHub Pages]

  classDef src fill:#E8EDBE,stroke:#08306B,color:#08306B
  classDef feat fill:#c5cbe0,stroke:#08306B,color:#08306B
  classDef model fill:#08306B,stroke:#08306B,color:#F7FBFF
  classDef out fill:#bcc47a,stroke:#08306B,color:#08306B
  class A,B,C,D src
  class F1,F2,F3,F4,Y,S feat
  class M,V1,V2 model
  class P,T1,T2,E,W,SITE out
```

## For Policy Making
From the city of Calgary, we can see that it faces the greatest risk of flooding during spring and summer. Calgary's 2013 flood displaced roughly 80,000 residents and remains the reference event for the city's flood planning. The Front Range of Colorado flooded the same year, with similar rainfall in the foothills. Additionally, heavy rainfall on the melting snowpack in the Rocky Mountains combined with steep, rocky terrain caused rapid and intense flooding in southern Alberta watersheds. Flooding disrupted businesses, damaged critical infrastructure, and caused power outages across Calgary. 

As a river city, it is important to prepare, respond, and adapt to floods. Every spring, the city of Calgary actively monitors the rivers for flooding. They continuously improve flood forecasting to provide citizens with the earliest possible warning. Therefore, the information from this analysis can be used by Calgary city planners to make informed decisions about land use, infrastructure development, and emergency preparedness. To deploy such an algorithm, we would first need to validate and refine the model using historical flood data and other relevant features. Once we have a model that fits well, we can use it to generate flood inundation maps for Calgary and comparable cities.

