# Neural Network Deployment steps

1. Train Neural network
2. Optimize Neural network
3. Deploy Application

---

## Step1. Train

### Train Neural network using Tensorflow, MATLAB, Keras, PyTorch, etc

Untrained Neural Network -> Training -> Trained Neural Network

---

## Step2. Optimize

### Optimize trained Neural network using Nvidia's TensorRT

Trained Neural Network -> TensorRT Optimizer -> Runtime PLAN file

- Workflow utilizes TensorRT for deployment
- Native support for TensorRT : TensorFlow, Matlab, keras
- TensorRT produces a PLAN file that
is a deployment optimized version
of the neural network
- PLAN file must be created on deployment architecture

### [ TensorFlow Example ]

1. Freeze Graph (make variables constants)
2. Convert DNN model to UFF file
3. Convert UFF file to Optimized PLAN file

---

## Step3. Deploy

### Deploy PLAN file using Deepwave's GR-Waveleaner and GNU Radio

Runtime PLAN file -> Waveleaner SDK -> SDR(GNU Radio)

---

> Ref : <https://deepwavedigital.com/wp-content/uploads/2019/09/GR-Wavelearner_Overview.pdf>  
