$$ \text{P} = \text{TP + FN} $$

$$ \text{N} = \text{TN + FP} $$

$$\text{Precision} =  \frac{\text{True Positives}}{\text{True Positives+False Positives}}$$


$$\text{Recall} = \text{TPR} = \frac{\text{True Positives}}{\text{True Positives+False Negatives}} = \frac{\text{TP}}{\text{P}}$$

$$\text{TNR} = \frac{\text{True Negatives}}{\text{True Negatives+False Positives}} = \frac{\text{TN}}{\text{N}}$$

$$\text{Accuracy} = \frac{\text{True Positives + True Negatives}}{\text{True Positives+ False Negatives + True Negatives+False Positives}} = \frac{\text{TP + TN}}{\text{P + N}}$$

# Loss functions and gradients

## MSE
Given a logistic activation function (sigmoid)


$$\frac{\partial \mathcal J}{\partial w_{k,d}^{(1)}}=\frac{2}{N}\sum_{n=1}^{N}(y^{[n]}-t^{[n]})w_k^{(2)}h_k^{[n]}(1-h_k^{[n]})x_d^{[n]}$$


$$\frac{\partial \mathcal J}{\partial w_{k}^{(2)}}=\frac{2}{N}\sum_{n=1}^{N}(y^{[n]}-t^{[n]})h_k^{[n]}$$

## BCE and CCE
without `2/N` at the beginning

## w.r.t. logits:

CCE with Softmax

Same as BCE with logistic activation function (sigmoid)

$$
\mathcal J^{\text{CCE}}
= -\frac{1}{N} \sum_{n=1}^{N} \log y_{\tau^{[n]}}^{[n]}
= -\frac{1}{N} \sum_{n=1}^{N} \log \frac{e^{z_{\tau^{[n]}}^{[n]} }}{\sum_{o=1}^{O} e^{z_o^{[n]} }}  
$$

$$
\frac{\partial\mathcal J^{[n]}}{\partial\mathcal z_o^{[n]}}
= -\frac{\partial \Bigl[ \sum_{o'=1}^{O} t_{o'}^{[n]}({z_{o'}^{[n]} }) - \log \sum_{o'=1}^{O} e^{{z_{o'}^{[n]} }}\Bigr]}{\partial z_o^{[n]}}\\[6ex]

= y_o^{[n]} -t_o^{[n]} 
$$

# Pytorch

## dims
0 - one column at a time

1 - one row at a time


```python
randints = torch.tensor([[-3,  9],
                         [ 1,  4],
                         [ 6,  2]])

randints.sum(dim=0) # separately for each column
>>
tensor([ 4, 15])

randints.sum(dim=1) # separately for each row
>>
tensor([6, 5, 8])

```



## Random numbers

Tensor of a defined shape `(3, 2)` of random **float32** numbers from `low` (-2) to `high` (3)

```python
torch.FloatTensor(3, 2).uniform_(-2, 3)

tensor([[0.4232, 0.7982],
        [2.0023, 0.6237],
        [0.9390, 0.1134]])
```

Another way:

```python
(low - high) * torch.rand(a, b) + high
```
e.g.

```python
(-2 - 3) * torch.rand(3, 2) + 3

tensor([[-1.9870, -0.7755],
        [-1.5575, -1.7540],
        [ 1.2621,  2.2252]])
```

Tensor of a defined shape `(3, 2)` of random **integers** from `low` (-2) to `high` (3)

```python
torch.randint(-2, 3, (3, 2))

tensor([[ 1,  0],
        [-1,  1],
        [-1, -1]])
```

## Pytorch Module

```python
class Network(torch.nn.Module):
    # D - number of input dimensions
    # K - number of hidden neurons
    # O - number of output dimensions
    def __init__(self, D, K, O):
        super(Network, self).__init__()
        self.fc1 = torch.nn.Linear(D, K)
        self.fc2 = torch.nn.Linear(K, O)
        self.a1 = torch.nn.Sigmoid()

    def forward(self, X):
        a = self.fc1(X)
        h = a1(a)
        z = self.fc2(h)
        y = tent(z) # tent is an activation function from exam
        return y

network = Network(2, 16, 1)
```

## Pytorch Sequential
Alternative: have to pass objects to `Sequential`, cannot pass `torch.nn.functional` function calls.

```python
model = torch.nn.Sequential(
        torch.nn.Linear(D, K),
        torch.nn.Sigmoid(),
        torch.nn.Linear(K, O)
)
```


## Pytorch Training Loop
```python
network = network.to(device)

optimizer = torch.optim.SGD(network.parameters(), lr=0.01, momentum=0.9)
loss = torch.nn.MSELoss()

network.train()
for iteration in range(10000):

    X, T = batch(1000)

    # train on batch
    X = X.to(device)
    T = T.to(device)
    Y = network(X)
    J = loss(Y, T)

    J.backward()
    optimizer.step()
    optimizer.zero_grad()  

    # access loss by .item()
    print(J.item())
```


## Pytorch Evaluation Loop
```python
model.eval()
val_loss, val_correct = 0, 0
with torch.no_grad():
    for x, t in val_loader:
        # Send the data to device
        x,t = x.to(device), t.to(device)
        # Get predictions
        z = model(x)
        # Compute validation loss
        J = loss_function(z,t)
        # Update the validation loss
        val_loss += J.item() * len(t)
        # Update the validation corrects
        preds = torch.argmax(z, dim=1)
        val_correct += (preds == t).sum().item()

# Store validation accuracy and loss for current epoch
avg_val_loss = val_loss/len(val_dataset)
val_acc = val_correct/len(val_dataset)
```

## Softmax

```python
sm = torch.nn.Softmax(dim=1)
sm(input)

# or

torch.nn.functional.softmax(input, dim=1)

```


## Convert Tensor to "normal"
```python
.item() # one item

.tolist() # a list

.numpy(force=True) # numpy ndarray
```

# Numpy

`concatentate` takes a tuple of arrays

```python
numpy.concatenate(([1], h_))
```

## Random numbers:

Using same trick as in pytorch, with r1, r2 (or low, high)

10 numbers from -2 to 2:

```python
(-2 - 2) * numpy.random.rand(10) + 2
>>
array([ 1.09914128,  1.24976012,  1.08751941, -1.25322792,  0.16843026,
       -0.59217607, -1.7445086 , -1.26549274,  1.76720579, -1.8669122 ])
```

or 
```python
numpy.random.uniform(-2, 2, 10)
```

# Convolutions

Spatial dimensions of feature maps after each layer:

$p$ is the padding (applied on both sides),

$U$ is the size of the kernel and 

$S$ is the stride.


Convolutional Layer:

$$
  \left\lfloor\frac{\text{Input} + 2 \cdot p - U}{S}\right\rfloor + 1 = \frac{28 - 7}{1} + 1 = 22 \times 22
$$

Max Pooling Layer

$$
\left\lfloor\frac{\text{Input}-U}{S} \right\rfloor + 1
= \frac{22-2}{2} + 1 = 11 \times 11
$$
