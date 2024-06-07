# Image Recognition Deep Learning Framework 

I wanted to write a notebook where I summarise all of the random procedure I've learnt from my many mistakes in the past year of deep learning for image recognition. The core of my learnings have come from error correcting, but I've found some of the most useful tools for not making dumb errors and understanding everything that I continously come back to are [Andrej Karpathy's Recipe](https://karpathy.github.io/2019/04/25/recipe/) and [Jeremy Howards FastAI Course](https://course.fast.ai/). With that being said, here is my current process (I may update my procedures in the future).

1. Download data which is ideal to do from within the Jupyter notebook. Create dataloaders based on the data structure. Use ImageFolder if data is organised by class folder.
2. Inspect the data. Often good to do within the notebook so its clear what the data looks like and what the distribution/ other features of the data are from within the notebook.
3. Train an initial model
   - Pick a simple architecture. As quoted from Karpathy, "Don't be a hero, use ResNet50". However, it is often good going for less computationally expensive architecture like ResNet36d which FastAI often used initially.
   - Pick an initial optimiser. Adam is best for initial testing as it is more robust than SGD
4. Tune features
   - Bring in data transforms. Simple ones initially and test whether they improve the loss. Vertical and horizontal flip (if appropriate) and rotations are typically good.
   - Data augmentations. Best practice here is to presize to larger image first and then perform some data augmentations and then do a resize crop (RandomResizeCrop in FastAI). This is because augmentations can lead to degradation and artefacts on the image edges.
   - Pick a larger deeper architecture. Here is where ResNet50 is generally the best option
   - Move to SGD at some point and tune learning rate for it.

I will update this more later
