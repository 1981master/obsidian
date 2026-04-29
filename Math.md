```
We begin by multiplying the input vector by the weight matrix to get the predicted output. Then, we compute the error by subtracting the prediction from the target. Next, we square these errors, sum them, and average them to get the mean squared error. After that, we compute the gradient by multiplying the error by the input, scale by 2, and average. Finally, we update the weights by subtracting the learning rate times the gradient. In short, this chain of matrix multiplication, error computation, squaring, averaging, and gradient descent is what drives the model to minimize loss and learn from the data.
```

$$  
\hat{y} = x \times W \\  
e_i = y_i - \hat{y}_i \\  
e_i^2 = (y_i - \hat{y}_i)^2 \\  
\text{MSE} = \frac{1}{N} \sum_{i=1}^{N} e_i^2 \\  
\frac{\partial \text{MSE}}{\partial W} = -\frac{2}{N} (x^T \times e) \\  
W_{\text{new}} = W_{\text{old}} - \eta \times \frac{\partial \text{MSE}}{\partial W}  
$$
