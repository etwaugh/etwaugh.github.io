# Is Fast AI actually Fast?

Doing both a thesis in machine learning and a course in deep learning, I've gotten the privilege of experimenting with different AI packages, PyTorch for the thesis and [FastAI](https://github.com/fastai/fastai) for my coursework. Initially I wondered if the idea for FastAI worked in practicality - does it actually increase the efficiency and simplicity of designing neural networks. The answer is *YES*.

Just comparing code snippets for model training in my thesis and my coursework is a crazy comparison.
PyTorch Model Train and Evaluate
```python
if not os.path.exists(MODEL_PATH) or RETRAIN:
    lr = 0.001
    momentum = 0.8
    step_size = 5
    gamma = 0.5
    #optimizer = torch.optim.Adam(model.parameters(), lr=lr)
    optimizer = torch.optim.SGD(model.parameters(), lr=lr, momentum=momentum)
    scheduler = torch.optim.lr_scheduler.StepLR(optimizer, step_size=step_size, gamma=gamma)
    cost = torch.nn.CrossEntropyLoss()
    n_epochs = 100
    for epoch in range(n_epochs):
        running_loss = 0.0
        running_correct = 0
        print("Epoch {}/{}".format(epoch, n_epochs))
        print("-"*10)
        #model.train()
        for data in data_loader_train:
            X_train, y_train = data
            if use_cuda:
                X_train, y_train = X_train.cuda(), y_train.cuda()
            outputs = F.softmax(model(X_train))
            optimizer.zero_grad()
            loss = cost(outputs, y_train)
            loss.backward()
            optimizer.step()
            running_loss += loss.item()
            _,pred = torch.max(outputs.data, 1)
            running_correct += torch.sum(pred == y_train.data).item()
        #model.eval()
        testing_correct = 0
        with torch.no_grad():
            for data in data_loader_test:
                X_test, y_test = data
                if use_cuda:
                    X_test, y_test = X_test.cuda(), y_test.cuda()
                outputs = model(X_test)
                _, pred = torch.max(outputs.data, 1)
                testing_correct += torch.sum(pred == y_test.data).item()
        print("Loss is:{:.8f}, Train Accuracy is:{:.2f}%, Test Accuracy is:{:.2f}%".format(running_loss*batch_size/len(train_dataset),
                                                                                          100*running_correct/len(train_dataset),
                                                                                          100*testing_correct/len(test_dataset)))
        scheduler.step()
```

FastAI Model Train and Evaluation
```python
learn = vision_learner(dls, resnet50, metrics=error_rate)
batch_size = 64
learn.dls[0].bs = batch_size
learn.fine_tune(10)
```

What initially took several weeks of debugging and optimising to tune hyperparameters is packed into a simple function that already includes best practices and can be done within a day! No need for struggling through low-level coding when you can just have high-level abstractions. And since it is integrated with PyTorch (the superior framework for ML), I don't need to do any extra package management. 

Needless to say, I am thoroughly enjoying progressing through the FastAI course as it progressively introduces newer and newer things. FastAI is definitely something I will continue to use for future.


