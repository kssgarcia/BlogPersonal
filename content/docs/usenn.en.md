---
title: How to upload NN
weight: 3
next: /docs/license
prev: /docs/howtorun
---

To download the model and use to predict values execute the following steps:

### Steps

{{% steps %}}

### Download weights

```python
import requests

# URL of the image to download
url = "https://neural-networks-weights.s3.us-east-2.amazonaws.com/unet.h5"

# Send an HTTP GET request to download the image
response = requests.get(url)

# Check if the request was successful (status code 200)
if response.status_code == 200:
    # Open a file in binary write mode and write the image content to it
    with open("unet.h5", "wb") as f:
        f.write(response.content)
    print("Image downloaded successfully!")
else:
    print("Failed to download the image. Status code:", response.status_code)
```

### Load the model

```python
from solidsopt.models import UNN_model

input_shape = (61, 61, 4)
model = UNN_model(input_shape)
model.load_weights('../models/best_models/best_matlab_detr_simple/cp.ckpt')
model.compile(optimizer='adam', loss='binary_crossentropy', metrics=['accuracy'])
```

### Run prediction

```python
result = model.predict(input)
```

### Plot the result
```python
plt.ion() 
fig,ax = plt.subplots()
ax.imshow(np.flipud(np.array(-result).reshape(60, 60)), cmap='gray', interpolation='none',norm=colors.Normalize(vmin=-1,vmax=0))
ax.set_title('Predicted')
fig.show()
```
{{% /steps %}}