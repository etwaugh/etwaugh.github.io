# What Race does AI say I am?

Since using [FastAI](https://github.com/fastai/fastai), it is now much easier to make quick and simple neural networks to do some predicting for me, and scraping using DuckDuckGo has made making datasets and dataloaders much easier too than downloading and formatting an external dataset. With this new found simplicity, I can now easily answer the question, what race does AI think I am?

To begin with, we'll construct a small list of 'races' according to what ChatGPT says for discriminatory ambiguity. ChatGPT ultimately decided on `caucasian, african, asian, native american, hispanic, pacific islander, middle eastern, aboriginal`

Training the model on 400 photos of each class then gives...

```python
learn = vision_learner(dls, resnet50, metrics=error_rate, loss_func=CrossEntropyLossFlat())
learn.fine_tune(10)
```
![image](https://github.com/etwaugh/etwaugh.github.io/assets/114034917/f2b01e55-3c70-4263-99e8-a94e5a6641b3)

![image](https://github.com/etwaugh/etwaugh.github.io/assets/114034917/47a2de56-0451-43e3-9052-9fee36683b9f)

![image](https://github.com/etwaugh/etwaugh.github.io/assets/114034917/51f6fe1f-e060-4519-bc8f-1518a3f239aa)

The model is alright, but still not the best. Nonetheless, we will test it on a young photo of me on the internet.

![image](https://github.com/etwaugh/etwaugh.github.io/assets/114034917/4d1014ed-3623-4e84-9d2d-37062f6885c8)

```python
# Predict on unseen data and show probability distribution
category,_,probs = learn.predict(PILImage.create('test.jpg'))
class_ordered = CIFAR10_classes.copy()
class_ordered.sort()
print(f"This is a {category}.\n")
print(f"Probabilities:")
for i in range(len(class_ordered)):
    print(f"   {class_ordered[i]}: {probs[i]:.4f}")
```
    This is a asian.
    Probabilities:
      aboriginal: 0.0000
      african: 0.0013
      asian: 0.9948
      caucasian: 0.0000
      hispanic: 0.0009
      middle eastern: 0.0007
      native american: 0.0014
      pacific islander: 0.0009

I guess I didn't really learn anything exciting from this so I'll probably have to test it on a different picture at another time

