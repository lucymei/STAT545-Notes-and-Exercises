# Special visualization analysis and design

### Nested model: Four levels of vis design

-domain situation
  - who are the target user
-abstraction
-idiom
  - how it is shown?
  
### Why is validation difficult?
- Solution: use methods from different fields at each level
- Domain situation - observe target users using existing tools
- Date/task abstraction
- Visual encoding/interaction idiom - justify design with respect to alternatives
- Algorithm - Meansure system time/memory, analyze computational complexity
- Analyze results qualitatively - Measure human time with lab experiment (lab study)
- Observe target users after depolyment (field study)
- Measure adoption

### Types: Datasets and data
1. Tables
2. Networks
3. Spatial
  - Fields (continuous)
  - Geometry (spatial)
  
- Ordering direction
  - Sequential
  - Diverging
  - Cyclic
  
- Attribute Types
  - Categorical
  - Ordered 
    - Ordinal
    - Quantitative 
    
### Actions: Analyze
- Consume
  - Discover vs Present (explore vs explain)
  - Enjoy

- Produce
  - annotate, record
  - dervie

- Analyze

### Derive
- don't just draw what you are given
  - decide what the right thing to show is
  - create it with a series of transformations from the original dataset
  - draw it
- one of the four major strategies for handling complexity
e.g. exports and imports plot as it is. we can do derive data by plotting trade balance = exports - imports.


### Actions: Analyze, Query

### Why: Targets
- All data
  - trends, outliers, features
  
- Attributes
  - one - distribution, extremes
  - many - dependency, correlation, similarity

- Network data
  - topology

- Spatial data
  - shape
  
### Definitions: Marks and channels
- marks 
  - geometric primitives

- channels
  - control appearance of marks
  - can redundantly code with multiple channels
  
### Visual encoding
- analyze idiom structure
  - as combination of marks and channels 

- Magnitude channels - how much
  - ordered attributes

- Identity channels - what kind of things
  - categorical attributes

- Expressivness principle
  - match channel and data characteristics
- Effectiveness principle
  - encode most important attributes with highest ranked channels
  - spatial position ranks high for both
  
### Accuracy: Fundamental Theory

### Discriminability: How many usable steps?
- must be sufficient for number of attribute levels to show
  - linewidth: few bins but salient
  
### Separability vs. Integrality

### Grouping
- containment
- connection
- proximity - same spatial region
- similarity - same values as other categorical channels

### Idiom design choices: Encode

### Categorical vs order color

### Decomposing color
- first rule of color: do not talk about color
  - color is confusing if treated as monolithic

- decompose into three channels
  - ordered can show magnitude
    - luminance: how bright
    - saturation: how colorful
  - categorical can show identity
    - hue: what color

- channels have different properties

### Categorical color: limited number of discriminable bins
- human perception built on relative comparisons
  - great if color contiguous 
  - surprisingly bad for absolute comparisons

- noncontiguous small region of color
  - fewer bins than you want 
  - rule of thumb: 6-12 bins, including background and highlights

### Ordered color: Rainbow is poor default
- problems - perceptually unordered, perceptually nonlinear
- benefits - fine-grained structure visible and nameable
- alternatives - large-scale structure: fewer hues
- luminance is what that is giving ordering

### Keys and values
- Key
  - independent attribute
  - used as unique index to look up items
  - simple tables: I key
  - multidimensional tables: multiple keys

### Idiom: scatterplot
- express values - quantittative attributes
- no keys, only values
  - good for finding trends, outliers, distribution, correlation, clusters
- scalability - hundreds of items

### Some keys: Categorical regions
- regions: contiguous bounded areas distinct from each other
  - using space to separate (proximity)
  - following expressiveness principle for categorical attributes
- use ordered attribute to order and align regions

### Idiom: bar chart
- one key, one value
- length to express quant value
- spatial regions: one per mark
- compare, lookup values
- scalability - dozens to hundreds of levels for key attribute

### Idion: line chart/ dot plot
- one key, one value
- 2 quant attributes
- line connection marks between them
- aligned lengths to express quant value
- separated and ordered by key attributes into horizontal regions
- find trend - connection marks emphasize ordering of items along key axis by explicitly showing relationship 

### Choosing bar vs line charts
- depends on type of key attributes
  - bar charts if categorical
  - line charts if ordered
- do not use line charts for categorical key attribs
  - violates expressiveness principle
  
### Idiom: heatmap
- two keys, one value
- 2 categ attribs
- q quant attrib
- marks - area, separate and align in 2D matrix
- channels - color by quant attrib
- find clusters, outliers
- scalability - IM items, 100s of categ levels, ~ 10 quant attrb levels
  - can have unlimited rows and columns but have limited values for the color coding
  
### Axis orientation

### Idioms: pie chart, polar area chart
- pie chart 
  - areamarks with angle channel
  - accuracy: angle/area less accurate than line length
- polar area chart 
  - area marks with length channel
  - more direct analog to bar charts

### Idioms: normalized stacked bar chart
- task 
  - part-to-whole judgements
- normalized stacked bar chart
  - stacked bar chart, normalized to full vert height
  - single stacked bar equivalent to full pie
- pie chart
  - information density: requires large circle
  
### Idiom: glyphmaps
- rectilinear good for linear vs nonlinear trends
- radial good for cyclic patterns

### Arrange spatial data
- Use given
  - geometry, spatial fields
  
### Idiom: choropleth map
- use given spatial data - when central task is understanding spatial relathionships
- data - geographic geometry, table with 1 quant attribute per region
- encoding
  - use given geometry for area mark boundaries
  - sequential segmented colormap
  - geographic heat maps
However,
- absolute vs relative again - population density vs per capita
- are you seeing attribute or just the population
- be careful when trying to normalize the capita data

### Idiom: Bayesian surprise maps
- use models of expectations to highlight surprising values
- confounds (population) and variance (sparsity)

### Arrange networks and trees

### Idiom: force-directed placement
- visual encoding - link connection marks, node point marks
- considerations 
  - spatial position: no meaning directly encoded
  - proximity semantics?
    - sometimes meaningful
    - sometimes arbitrary, artifcat of layout algorithm
    - tension with length
- explore topology; locate paths, clusters
- scalability - node/edge density E < 4N

### Idiom: adjacency matrix view
- transform into same data/encoding as heatmap
- derived data: table from network
  - 1 quant
  - 2 categ attributes
- cell shows presence/absence of edge

### Connection vs. adjacency comparison
- adjacency matrix strengths
- node-link diagram strengths
- empriical study

### Link marks: Connection and containment
- marks as links (vs. nodes)
  - common case in network drawing
  - 1D case: connection
    - emhasizes topology, path tracing
    - networks and trees
  - 2D case: containment
      - emphasizes attrib values at leaves (size coding)
      - only trees
      
### How to handle complexity: 1 previous strategy + 3 more
- derive new data to show within view
- change view over time
- facet across multiple views
- reduce items/attributes within single view

