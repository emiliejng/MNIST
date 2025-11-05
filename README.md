Digit Classifier — Tinygrad + WebGPU


Live Demo

<img width="1440" height="900" alt="Capture d’écran 2025-11-05 à 03 41 09" src="https://github.com/user-attachments/assets/5636f329-24e9-4f40-846f-2c46f8e2a597" />

Try the live app on GitHub Pages :
https://emiliejng.github.io/MNIST/


Overview

This project demonstrates how to train deep learning models in Python using Tinygrad, export them, and run them directly inside a WebGPU-based web app.

It recognizes handwritten digits (0–9) in real time.
You can draw a digit on the canvas, and the model instantly predicts the number with confidence bars.

The main goal is to connect Tinygrad (for training) with WebGPU (for inference) to build a fully functional browser-based AI demo.


Features:

- Two trained models:
MLP (Multi-Layer Perceptron)
CNN (Convolutional Neural Network)

- Interactive drawing canvas with Pen, Eraser, and Clear tools

- Real-time predictions with WebGPU acceleration

- Probability bar chart showing softmax confidence for digits 0–9

- Displays inference time (ms) for each prediction

- Responsive design with Tailwind CSS

- Runs locally or online via GitHub Pages

- Model selector to switch between MLP and CNN


Model Summary: 

Model Name	Architecture	Accuracy	Training Settings
mnist_mlp	MLP (3 dense layers)	accuracy:97.89%	LR=0.025, Batch=512, Steps=350
mnist_convnet	CNN (3 conv + 2 dense layers)	accuracy:98.95%	LR=0.015, Batch=512, Steps=250

More experiment results can be found here : HYPERPARAMETERS.md


Setup / Local Run:

To test the project locally:

Clone this repository
git clone https://github.com/emiliejng/MNIST.git
cd tinygrad-webgpu

Start a local server
WebGPU requires an HTTP server (not file://):
python -m http.server

Open in your browser
http://localhost:8000

Make sure WebGPU is enabled (see below for Safari setup).


Enabling WebGPU on Safari (Mac)
Install Safari Technology Preview → Download here
Go to Preferences → Advanced → Show Develop menu
In the Develop menu, go to Experimental Features → enable WebGPU
Reload your app at http://localhost:8000
On Chrome: go to chrome://flags/#enable-unsafe-webgpu → Enable → Relaunch


Hyperparameter Log
All training experiments, configurations, and accuracies are recorded in
👉 HYPERPARAMETERS.md :
https://github.com/emiliejng/MNIST/blob/main/HYPERPARAMETERS.md


Summary
This project connects Tinygrad training with WebGPU inference in a single page web app.
It proves that deep learning models can run fully on the browser GPU without external servers.
Both MLP and CNN achieve strong accuracy and real time performance.
  
