# EDI-Mathematical-model

## Model for SIGHT 
## Input:

- **Input Image:** Denoted by X

### Processing Stages:

#### 1. Feature Extraction Backbone:

- **Convolutional Layer Operation:**

  - **Input:** Feature map X
  - **Output:** Feature map Y
  - **Equation:**
    - Y(i, j) = Σ(u, v) X(i+u, j+v) \* W(u, v)

- **Max Pooling Operation:**
  - **Input:** Feature map X
  - **Output:** Downsampled feature map Y
  - **Equation:**
    - Y(i, j) = max(u, v) X(i+u, j+v)

#### 2. Object Detection Head:

- **Detection Layer Operation:**
  - **Input:** Feature map X
  - **Output:**
    - Bounding box coordinates bbox(i,j)
    - Objectness score conf(i,j)
    - Class probabilities class(i,j,c)
  - **Equation:**
    - bbox(i,j) = (tx(i,j) _ σ(tw(i,j)) + b(i,j), ty(i,j) _ σ(th(i,j)) + b(i,j))
    - conf(i,j) = σ(tc(i,j))
    - class(i,j,c) = pc(i,j,c) \* σ(t_c(i,j,c))

#### 3. Anchor Boxes:

- **Anchor Box Calculation:**
  - **Input:** None (Derived from the network)
  - **Output:** Anchor box dimensions w_a, h_a
  - **Equation:**
    - w_a = p_wa \* e^(t_w)
    - h_a = p_ha \* e^(t_h)

#### 4. Non-Maximum Suppression (NMS):

- **Input:** Set of bounding boxes B, Score threshold Σ, Intersection over Union threshold T
- **Output:** Selected bounding boxes β_i in B after NMS
- **Equation:**
  - NMS(B, Σ, T) = { β_i in B | ∀ β_i, β_j in B, i ≠ j: IoU(β_i, β_j) < T }

## Output:

- **Final Output:** Selected bounding boxes after NMS
