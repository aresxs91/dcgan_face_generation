# dcgan_face_generation

The architecture used here to generate realistic face images out of the [celeba](http://mmlab.ie.cuhk.edu.hk/projects/CelebA.html) dataset is based on the DCGAN (paper)[https://arxiv.org/abs/1511.06434] with a few additions/changes:

1. Adding dropout in the intermediary layers of the generator (small probability of dropping nodes) so that it is less prone to learning the data distribution.
2. All *intermediary* layers use leaky RELU activations to avoid sparse gradients (~ 0 gradients). Leaky ReLU allows gradients to flow backwards through the layer unimpeded.
3. Image to be generated had to be a 28x28x5, so the first, fully connected layer on the generator had to start from a 7x7 image width and height for obvious reasons
4. The weight initialisation stayed the same although some experimentation showed that using the "Xavier" initialization would keep the layer scales stable throughout (uses a uniform distribution). Not much performance gain from the experiments done offline so I left this out
5. To keep the generator's architecture identical to the DCGAN paper, keeping all original 4 intermediary layers, with the last convolution to use a stride of 1, so to not alter the image's shape.
6. Beta1 variable was set a bit higher than required here, ~0.1 might produce even better results.
